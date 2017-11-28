---
title: "Öğretici: Azure Active Directory Tümleştirme ile Work.com | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Work.com arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="d83ac-103">Öğretici: Azure Active Directory Tümleştirme Work.com ile</span><span class="sxs-lookup"><span data-stu-id="d83ac-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="d83ac-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Work.com tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d83ac-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d83ac-105">Work.com Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d83ac-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d83ac-106">Work.com erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d83ac-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="d83ac-107">Otomatik olarak için Work.com (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d83ac-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d83ac-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d83ac-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d83ac-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d83ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d83ac-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d83ac-110">Prerequisites</span></span>

<span data-ttu-id="d83ac-111">Azure AD tümleştirme Work.com ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="d83ac-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="d83ac-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d83ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d83ac-113">Bir Work.com çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="d83ac-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d83ac-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d83ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d83ac-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d83ac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d83ac-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d83ac-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d83ac-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d83ac-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d83ac-118">Scenario description</span></span>
<span data-ttu-id="d83ac-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d83ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d83ac-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d83ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d83ac-121">Galeriden Work.com Ekle</span><span class="sxs-lookup"><span data-stu-id="d83ac-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="d83ac-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d83ac-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="d83ac-123">Galeriden Work.com Ekle</span><span class="sxs-lookup"><span data-stu-id="d83ac-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="d83ac-124">Azure AD Work.com tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Work.com eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d83ac-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d83ac-125">**Galeriden Work.com eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d83ac-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d83ac-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d83ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d83ac-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d83ac-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d83ac-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d83ac-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d83ac-133">Arama kutusuna **Work.com**seçin **Work.com** sonuçları panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="d83ac-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![Galerisi'nden ekleme](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d83ac-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d83ac-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d83ac-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Work.com sınayın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d83ac-137">Tekli çalışmaya oturum için Azure AD Work.com karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="d83ac-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="d83ac-138">Diğer bir deyişle, bir Azure AD kullanıcısının Work.com ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d83ac-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="d83ac-139">Work.com içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="d83ac-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d83ac-140">Yapılandırma ve Azure AD çoklu oturum açma Work.com ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d83ac-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d83ac-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d83ac-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d83ac-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="d83ac-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d83ac-143">**[Work.com test kullanıcısı oluşturma](#create-a-workcom-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Work.com sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="d83ac-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d83ac-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d83ac-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d83ac-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d83ac-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d83ac-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d83ac-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Work.com uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="d83ac-148">Çoklu oturum açma yapılandırmak için özel bir Work.com etki alanı adı henüz Kurulum gerekir.</span><span class="sxs-lookup"><span data-stu-id="d83ac-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="d83ac-149">En az bir etki alanı adı tanımlayın, etki alanı adınızı sınamak ve kuruluşunuzun tümüne dağıtmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="d83ac-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="d83ac-150">**Azure AD çoklu oturum açma ile Work.com yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d83ac-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="d83ac-151">Azure portalında üzerinde **Work.com** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d83ac-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d83ac-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML tabanlı oturum açma](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="d83ac-155">Üzerinde **Work.com etki alanı ve URL'leri** bölümünde, aşağıdaki işlemi gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d83ac-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Work.com etki alanı ve URL'ler bölümü](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="d83ac-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="d83ac-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d83ac-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="d83ac-158">This value is not real.</span></span> <span data-ttu-id="d83ac-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d83ac-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d83ac-160">Kişi [Work.com istemci destek ekibi](https://help.salesforce.com/articleView?id=000159855&type=3) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="d83ac-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="d83ac-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d83ac-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="d83ac-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d83ac-163">Click **Save** button.</span></span>

    ![Kaydet Düğmesi](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d83ac-165">Üzerinde **Work.com yapılandırma** 'yi tıklatın **yapılandırma Work.com** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d83ac-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d83ac-166">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="d83ac-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Work.com yapılandırma bölümü](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="d83ac-168">Work.com Kiracı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="d83ac-169">Git **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="d83ac-170">![Kurulum](./media/active-directory-saas-work-com-tutorial/ic794108.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="d83ac-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="d83ac-171">Sol gezinti bölmesinde, içinde **Yönet** 'yi tıklatın **etki alanı yönetimi** ilgili bölümü genişletin ve ardından **My etki alanı** açmak için **My etki alanı** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d83ac-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="d83ac-172">![Etki alanım](./media/active-directory-saas-work-com-tutorial/ic767825.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="d83ac-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="d83ac-173">Etki alanınızın doğru şekilde ayarlanmış olması gerektiğini doğrulamak için içinde olduğundan emin olun "**adım 4 dağıtılan kullanıcılara**" ve gözden geçirin, "**My etki alanı ayarları**".</span><span class="sxs-lookup"><span data-stu-id="d83ac-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="d83ac-174">![Etki alanı kullanıcıya dağıtılan](./media/active-directory-saas-work-com-tutorial/ic784377.png "kullanıcıya dağıtılan etki alanı")</span><span class="sxs-lookup"><span data-stu-id="d83ac-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="d83ac-175">Work.com kiracınız için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="d83ac-176">Git **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="d83ac-177">![Kurulum](./media/active-directory-saas-work-com-tutorial/ic794108.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="d83ac-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="d83ac-178">Genişletme **güvenlik denetimleri** menüsüne ve ardından **çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="d83ac-179">![Çoklu oturum açma ayarları](./media/active-directory-saas-work-com-tutorial/ic794113.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="d83ac-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="d83ac-180">Üzerinde **çoklu oturum açma ayarları** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d83ac-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="d83ac-181">![SAML etkin](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML etkin")</span><span class="sxs-lookup"><span data-stu-id="d83ac-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="d83ac-182">a.</span><span class="sxs-lookup"><span data-stu-id="d83ac-182">a.</span></span> <span data-ttu-id="d83ac-183">Seçin **SAML etkin**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="d83ac-184">b.</span><span class="sxs-lookup"><span data-stu-id="d83ac-184">b.</span></span> <span data-ttu-id="d83ac-185">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-185">Click **New**.</span></span>

15. <span data-ttu-id="d83ac-186">İçinde **SAML çoklu oturum açma ayarları** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d83ac-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="d83ac-187">![Oturum açma SAML tek ayar](./media/active-directory-saas-work-com-tutorial/ic794114.png "oturum açma SAML tek ayar")</span><span class="sxs-lookup"><span data-stu-id="d83ac-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="d83ac-188">a.</span><span class="sxs-lookup"><span data-stu-id="d83ac-188">a.</span></span> <span data-ttu-id="d83ac-189">İçinde **adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="d83ac-190">İçin bir değer sağlama **adı** otomatik olarak doldurulması **API adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d83ac-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="d83ac-191">b.</span><span class="sxs-lookup"><span data-stu-id="d83ac-191">b.</span></span> <span data-ttu-id="d83ac-192">İçinde **veren** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d83ac-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="d83ac-193">c.</span><span class="sxs-lookup"><span data-stu-id="d83ac-193">c.</span></span> <span data-ttu-id="d83ac-194">Azure Portalı'ndan indirilen sertifikayı karşıya yüklemek için tıklayın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="d83ac-195">d.</span><span class="sxs-lookup"><span data-stu-id="d83ac-195">d.</span></span> <span data-ttu-id="d83ac-196">İçinde **varlık kimliği** metin kutusuna, türü `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="d83ac-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="d83ac-197">e.</span><span class="sxs-lookup"><span data-stu-id="d83ac-197">e.</span></span> <span data-ttu-id="d83ac-198">Olarak **SAML kimlik türü**seçin **onaylamayı içeren kullanıcı nesnesinden Federasyon kimliği**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="d83ac-199">f.</span><span class="sxs-lookup"><span data-stu-id="d83ac-199">f.</span></span> <span data-ttu-id="d83ac-200">Olarak **SAML kimlik konumu**seçin **kimliktir konu deyimi NameIdentfier öğesinde**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="d83ac-201">g.</span><span class="sxs-lookup"><span data-stu-id="d83ac-201">g.</span></span> <span data-ttu-id="d83ac-202">İçinde **kimlik sağlayıcısı oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d83ac-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d83ac-203">h.</span><span class="sxs-lookup"><span data-stu-id="d83ac-203">h.</span></span> <span data-ttu-id="d83ac-204">İçinde **kimlik sağlayıcısı oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d83ac-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="d83ac-205">ı.</span><span class="sxs-lookup"><span data-stu-id="d83ac-205">i.</span></span> <span data-ttu-id="d83ac-206">Olarak **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="d83ac-207">j.</span><span class="sxs-lookup"><span data-stu-id="d83ac-207">j.</span></span> <span data-ttu-id="d83ac-208">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-208">Click **Save**.</span></span>

16. <span data-ttu-id="d83ac-209">Sol gezinti bölmesinde, Work.com Klasik Portalı'nda tıklatın **etki alanı yönetimi** ilgili bölümü genişletin ve ardından **My etki alanı** açmak için **My etki alanı** Sayfa.</span><span class="sxs-lookup"><span data-stu-id="d83ac-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="d83ac-210">![Etki alanım](./media/active-directory-saas-work-com-tutorial/ic794115.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="d83ac-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="d83ac-211">Üzerinde **My etki alanı** sayfasında **oturum açma sayfası markalama** 'yi tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="d83ac-212">![Oturum açma sayfası markalama](./media/active-directory-saas-work-com-tutorial/ic767826.png "oturum açma sayfası markalama")</span><span class="sxs-lookup"><span data-stu-id="d83ac-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="d83ac-213">Üzerinde **oturum açma sayfası markalama** sayfasında **kimlik doğrulama hizmeti** bölümünde, adını, **SAML SSO ayarları** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d83ac-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="d83ac-214">Seçin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="d83ac-215">![Oturum açma sayfası markalama](./media/active-directory-saas-work-com-tutorial/ic784366.png "oturum açma sayfası markalama")</span><span class="sxs-lookup"><span data-stu-id="d83ac-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="d83ac-216">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d83ac-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d83ac-217">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="d83ac-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d83ac-218">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d83ac-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d83ac-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d83ac-219">Create an Azure AD test user</span></span>
<span data-ttu-id="d83ac-220">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d83ac-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d83ac-222">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d83ac-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d83ac-223">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d83ac-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d83ac-225">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Kullanıcıların ve grupların tüm kullanıcılar ->](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d83ac-227">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="d83ac-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Ekle](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d83ac-229">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d83ac-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Kullanıcı iletişim sayfası](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d83ac-231">a.</span><span class="sxs-lookup"><span data-stu-id="d83ac-231">a.</span></span> <span data-ttu-id="d83ac-232">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d83ac-233">b.</span><span class="sxs-lookup"><span data-stu-id="d83ac-233">b.</span></span> <span data-ttu-id="d83ac-234">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d83ac-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d83ac-235">c.</span><span class="sxs-lookup"><span data-stu-id="d83ac-235">c.</span></span> <span data-ttu-id="d83ac-236">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d83ac-237">d.</span><span class="sxs-lookup"><span data-stu-id="d83ac-237">d.</span></span> <span data-ttu-id="d83ac-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="d83ac-239">Work.com test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d83ac-239">Create a Work.com test user</span></span>
<span data-ttu-id="d83ac-240">Azure Active Directory kullanıcıların oturum açabilmesi için bunlar için Work.com sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d83ac-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="d83ac-241">Work.com söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="d83ac-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="d83ac-242">Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d83ac-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="d83ac-243">Work.com şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d83ac-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="d83ac-244">Git **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="d83ac-245">![Kurulum](./media/active-directory-saas-work-com-tutorial/IC794108.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="d83ac-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="d83ac-246">Git **kullanıcıları yönetme \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="d83ac-247">![Kullanıcıları yönetme](./media/active-directory-saas-work-com-tutorial/IC784369.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="d83ac-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="d83ac-248">Tıklatın **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-248">Click **New User**.</span></span>
   
    <span data-ttu-id="d83ac-249">![Tüm kullanıcılar](./media/active-directory-saas-work-com-tutorial/IC794117.png "tüm kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="d83ac-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="d83ac-250">Kullanıcı düzenleme bölümünde, aşağıdaki adımlarda, geçerli bir Azure özniteliklerini gerçekleştirmek istediğiniz ilgili metin kutularına sağlamayı AD hesabı:</span><span class="sxs-lookup"><span data-stu-id="d83ac-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="d83ac-251">![Kullanıcı düzenleme](./media/active-directory-saas-work-com-tutorial/ic794118.png "kullanıcı düzenleme")</span><span class="sxs-lookup"><span data-stu-id="d83ac-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="d83ac-252">a.</span><span class="sxs-lookup"><span data-stu-id="d83ac-252">a.</span></span> <span data-ttu-id="d83ac-253">İçinde **ad** metin kutusuna, türü **ad** kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="d83ac-254">b.</span><span class="sxs-lookup"><span data-stu-id="d83ac-254">b.</span></span> <span data-ttu-id="d83ac-255">İçinde **Soyadı** metin kutusuna, türü **Soyadı** kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="d83ac-256">c.</span><span class="sxs-lookup"><span data-stu-id="d83ac-256">c.</span></span> <span data-ttu-id="d83ac-257">İçinde **diğer** metin kutusuna, türü **adı** kullanıcının **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="d83ac-258">d.</span><span class="sxs-lookup"><span data-stu-id="d83ac-258">d.</span></span> <span data-ttu-id="d83ac-259">İçinde **e-posta** metin kutusuna, türü **e-posta adresi** kullanıcının  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="d83ac-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="d83ac-260">e.</span><span class="sxs-lookup"><span data-stu-id="d83ac-260">e.</span></span> <span data-ttu-id="d83ac-261">İçinde **kullanıcı adı** metin kutusuna, türü kullanıcının kullanıcı adını ister  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="d83ac-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="d83ac-262">f.</span><span class="sxs-lookup"><span data-stu-id="d83ac-262">f.</span></span> <span data-ttu-id="d83ac-263">İçinde **takma ad** metin kutusuna, bir **takma ad** kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="d83ac-264">g.</span><span class="sxs-lookup"><span data-stu-id="d83ac-264">g.</span></span> <span data-ttu-id="d83ac-265">Seçin **rol**, **kullanıcı lisansı**, ve **profil**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="d83ac-266">h.</span><span class="sxs-lookup"><span data-stu-id="d83ac-266">h.</span></span> <span data-ttu-id="d83ac-267">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d83ac-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="d83ac-268">Azure AD hesap sahibi etkin duruma gelmesi hesabı onaylamak için bir bağlantı içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d83ac-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d83ac-269">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="d83ac-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="d83ac-270">Bu bölümde, Britta Work.com için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d83ac-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d83ac-272">**Work.com için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d83ac-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="d83ac-273">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d83ac-275">Uygulamalar listesinde **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-275">In the applications list, select **Work.com**.</span></span>

    ![Uygulamanın listesinde Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="d83ac-277">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d83ac-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d83ac-279">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d83ac-279">Click **Add** button.</span></span> <span data-ttu-id="d83ac-280">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d83ac-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d83ac-282">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d83ac-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d83ac-283">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d83ac-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d83ac-284">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d83ac-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d83ac-285">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="d83ac-285">Test single sign-on</span></span>

<span data-ttu-id="d83ac-286">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d83ac-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d83ac-287">Erişim paneli Work.com parçasında tıklattığınızda, otomatik olarak Work.com uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="d83ac-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="d83ac-288">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d83ac-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d83ac-289">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d83ac-289">Additional resources</span></span>

* [<span data-ttu-id="d83ac-290">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="d83ac-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d83ac-291">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d83ac-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

