---
title: "Öğretici: Azure Active Directory Tümleştirme ile TargetProcess | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile TargetProcess arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: d15931a5d430252bbd9ae342e1f8fde1a539355b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="70cf0-103">Öğretici: Azure Active Directory Tümleştirme TargetProcess ile</span><span class="sxs-lookup"><span data-stu-id="70cf0-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="70cf0-104">Bu öğreticide, Azure Active Directory (Azure AD) ile TargetProcess tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="70cf0-104">In this tutorial, you learn how to integrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70cf0-105">TargetProcess Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="70cf0-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="70cf0-106">TargetProcess erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="70cf0-106">You can control in Azure AD who has access to TargetProcess</span></span>
- <span data-ttu-id="70cf0-107">Otomatik olarak için TargetProcess (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="70cf0-107">You can enable your users to automatically get signed-on to TargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70cf0-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="70cf0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="70cf0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70cf0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70cf0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="70cf0-110">Prerequisites</span></span>

<span data-ttu-id="70cf0-111">Azure AD tümleştirme TargetProcess ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="70cf0-111">To configure Azure AD integration with TargetProcess, you need the following items:</span></span>

- <span data-ttu-id="70cf0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="70cf0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70cf0-113">Bir TargetProcess çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="70cf0-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70cf0-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="70cf0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70cf0-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="70cf0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70cf0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="70cf0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70cf0-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70cf0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70cf0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="70cf0-118">Scenario description</span></span>
<span data-ttu-id="70cf0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="70cf0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70cf0-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="70cf0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70cf0-121">Galeriden TargetProcess Ekle</span><span class="sxs-lookup"><span data-stu-id="70cf0-121">Add TargetProcess from the gallery</span></span>
2. <span data-ttu-id="70cf0-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="70cf0-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-the-gallery"></a><span data-ttu-id="70cf0-123">Galeriden TargetProcess Ekle</span><span class="sxs-lookup"><span data-stu-id="70cf0-123">Add TargetProcess from the gallery</span></span>
<span data-ttu-id="70cf0-124">Azure AD TargetProcess tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden TargetProcess eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="70cf0-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="70cf0-125">**Galeriden TargetProcess eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="70cf0-125">**To add TargetProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="70cf0-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="70cf0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70cf0-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="70cf0-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="70cf0-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="70cf0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="70cf0-133">Arama kutusuna **TargetProcess**seçin **TargetProcess** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="70cf0-133">In the search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button to add the application.</span></span>

    ![Galeriden Ekle TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="70cf0-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="70cf0-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="70cf0-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı TargetProcess sınayın.</span><span class="sxs-lookup"><span data-stu-id="70cf0-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="70cf0-137">Tekli çalışmaya oturum için Azure AD TargetProcess karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="70cf0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TargetProcess is to a user in Azure AD.</span></span> <span data-ttu-id="70cf0-138">Diğer bir deyişle, bir Azure AD kullanıcısının TargetProcess ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="70cf0-138">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span></span>

<span data-ttu-id="70cf0-139">TargetProcess içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="70cf0-139">In TargetProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="70cf0-140">Yapılandırma ve Azure AD çoklu oturum açma TargetProcess ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="70cf0-140">To configure and test Azure AD single sign-on with TargetProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="70cf0-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="70cf0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="70cf0-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="70cf0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70cf0-143">**[TargetProcess test kullanıcısı oluşturma](#create-a-targetprocess-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı TargetProcess sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="70cf0-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="70cf0-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="70cf0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70cf0-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="70cf0-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="70cf0-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="70cf0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="70cf0-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma TargetProcess uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="70cf0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="70cf0-148">**Azure AD çoklu oturum açma ile TargetProcess yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="70cf0-148">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="70cf0-149">Azure portalında üzerinde **TargetProcess** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-149">In the Azure portal, on the **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="70cf0-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="70cf0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML tabanlı oturum açma](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="70cf0-153">Üzerinde **TargetProcess etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="70cf0-153">On the **TargetProcess Domain and URLs** section, perform the following steps:</span></span>

    ![TargetProcess etki alanı ve URL'ler bölümü](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="70cf0-155">a.</span><span class="sxs-lookup"><span data-stu-id="70cf0-155">a.</span></span> <span data-ttu-id="70cf0-156">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="70cf0-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="70cf0-157">b.</span><span class="sxs-lookup"><span data-stu-id="70cf0-157">b.</span></span> <span data-ttu-id="70cf0-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="70cf0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70cf0-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="70cf0-159">These values are not real.</span></span> <span data-ttu-id="70cf0-160">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="70cf0-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="70cf0-161">Kişi [TargetProcess istemci destek ekibi](mailto:support@targetprocess.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="70cf0-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) to get these values.</span></span> 
 
4. <span data-ttu-id="70cf0-162">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="70cf0-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="70cf0-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="70cf0-164">Click **Save** button.</span></span>

    ![Kaydet düğmesi](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="70cf0-166">Üzerinde **TargetProcess yapılandırma** 'yi tıklatın **yapılandırma TargetProcess** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="70cf0-166">On the **TargetProcess Configuration** section, click **Configure TargetProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="70cf0-167">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="70cf0-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TargetProcess yapılandırma bölümü](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="70cf0-169">Yönetici olarak TargetProcess uygulamanıza oturum.</span><span class="sxs-lookup"><span data-stu-id="70cf0-169">Sign-on to your TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="70cf0-170">Üstteki menüde tıklatın **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-170">In the menu on the top, click **Setup**.</span></span>
   
    ![Kurulum](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="70cf0-172">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-172">Click **Settings**.</span></span>
   
    ![Ayarlar](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="70cf0-174">Tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-174">Click **Single Sign-on**.</span></span>
   
    ![Çoklu oturum açma'ı tıklatın](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="70cf0-176">Çoklu oturum açma ayarları iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="70cf0-176">On the Single Sign-on settings dialog, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="70cf0-178">a.</span><span class="sxs-lookup"><span data-stu-id="70cf0-178">a.</span></span> <span data-ttu-id="70cf0-179">Tıklatın **çoklu oturum açmayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="70cf0-180">b.</span><span class="sxs-lookup"><span data-stu-id="70cf0-180">b.</span></span> <span data-ttu-id="70cf0-181">İçinde **oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="70cf0-181">In **Sign-on URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="70cf0-182">c.</span><span class="sxs-lookup"><span data-stu-id="70cf0-182">c.</span></span> <span data-ttu-id="70cf0-183">İndirilen sertifikanızı Not Defteri'nde açın, içeriği Kopyala ve ardından yapıştırın **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="70cf0-183">Open your downloaded certificate in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="70cf0-184">d.</span><span class="sxs-lookup"><span data-stu-id="70cf0-184">d.</span></span> <span data-ttu-id="70cf0-185">tıklatın **JIT etkinleştirme sağlama**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="70cf0-186">e.</span><span class="sxs-lookup"><span data-stu-id="70cf0-186">e.</span></span> <span data-ttu-id="70cf0-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="70cf0-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="70cf0-188">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="70cf0-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="70cf0-189">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="70cf0-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="70cf0-190">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70cf0-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="70cf0-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="70cf0-191">Create an Azure AD test user</span></span>
<span data-ttu-id="70cf0-192">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="70cf0-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="70cf0-194">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="70cf0-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="70cf0-195">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="70cf0-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70cf0-197">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Kullanıcıların listesini görüntülemek için](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70cf0-199">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="70cf0-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Ekle düğmesi](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70cf0-201">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="70cf0-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Kullanıcı bölümü](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70cf0-203">a.</span><span class="sxs-lookup"><span data-stu-id="70cf0-203">a.</span></span> <span data-ttu-id="70cf0-204">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70cf0-205">b.</span><span class="sxs-lookup"><span data-stu-id="70cf0-205">b.</span></span> <span data-ttu-id="70cf0-206">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="70cf0-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70cf0-207">c.</span><span class="sxs-lookup"><span data-stu-id="70cf0-207">c.</span></span> <span data-ttu-id="70cf0-208">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="70cf0-209">d.</span><span class="sxs-lookup"><span data-stu-id="70cf0-209">d.</span></span> <span data-ttu-id="70cf0-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="70cf0-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="70cf0-211">TargetProcess test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="70cf0-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="70cf0-212">Bu bölümün amacı Britta Simon içinde TargetProcess adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="70cf0-212">The objective of this section is to create a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="70cf0-213">Yalnızca zaman sağlama TargetProcess destekler.</span><span class="sxs-lookup"><span data-stu-id="70cf0-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="70cf0-214">İçinde zaten etkinleştirdiğiniz [yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="70cf0-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="70cf0-215">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="70cf0-215">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="70cf0-216">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="70cf0-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="70cf0-217">Bu bölümde, Britta TargetProcess için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="70cf0-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TargetProcess.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="70cf0-219">**TargetProcess için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="70cf0-219">**To assign Britta Simon to TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="70cf0-220">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="70cf0-222">Uygulamalar listesinde **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-222">In the applications list, select **TargetProcess**.</span></span>

    ![Uygulama listesinde TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="70cf0-224">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="70cf0-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="70cf0-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="70cf0-226">Click **Add** button.</span></span> <span data-ttu-id="70cf0-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="70cf0-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="70cf0-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="70cf0-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="70cf0-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="70cf0-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70cf0-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="70cf0-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="70cf0-232">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="70cf0-232">Test single sign-on</span></span>

<span data-ttu-id="70cf0-233">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="70cf0-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="70cf0-234">Erişim paneli TargetProcess parçasında tıklattığınızda, otomatik olarak TargetProcess uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="70cf0-234">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span></span> <span data-ttu-id="70cf0-235">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="70cf0-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70cf0-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="70cf0-236">Additional resources</span></span>

* [<span data-ttu-id="70cf0-237">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="70cf0-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70cf0-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="70cf0-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

