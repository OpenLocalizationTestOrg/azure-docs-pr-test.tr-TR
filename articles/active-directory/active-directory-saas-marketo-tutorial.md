---
title: "Öğretici: Azure Active Directory Tümleştirme ile Marketo | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Marketo arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e146fd5a8075bc9c7ba049b25e5f301fc2645ed9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="edd4f-103">Öğretici: Marketo Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="edd4f-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="edd4f-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Marketo tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="edd4f-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edd4f-105">Marketo Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="edd4f-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="edd4f-106">Marketo erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="edd4f-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="edd4f-107">Otomatik olarak için Marketo (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="edd4f-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="edd4f-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="edd4f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="edd4f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="edd4f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edd4f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="edd4f-110">Prerequisites</span></span>

<span data-ttu-id="edd4f-111">Azure AD tümleştirme Marketo ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="edd4f-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="edd4f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="edd4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edd4f-113">Bir Marketo çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="edd4f-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="edd4f-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="edd4f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="edd4f-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="edd4f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edd4f-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="edd4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="edd4f-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edd4f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edd4f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="edd4f-118">Scenario description</span></span>
<span data-ttu-id="edd4f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="edd4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="edd4f-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="edd4f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edd4f-121">Galeriden Marketo ekleme</span><span class="sxs-lookup"><span data-stu-id="edd4f-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="edd4f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="edd4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="edd4f-123">Galeriden Marketo ekleme</span><span class="sxs-lookup"><span data-stu-id="edd4f-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="edd4f-124">Azure AD Marketo tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Marketo eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="edd4f-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="edd4f-125">**Galeriden Marketo eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="edd4f-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="edd4f-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="edd4f-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="edd4f-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="edd4f-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="edd4f-133">Arama kutusuna **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-133">In the search box, type **Marketo**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="edd4f-135">Sonuçlar panelinde seçin **Marketo**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="edd4f-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="edd4f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="edd4f-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Marketo ile test etme</span><span class="sxs-lookup"><span data-stu-id="edd4f-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="edd4f-139">Tekli çalışmaya oturum için Azure AD Marketo karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="edd4f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="edd4f-140">Diğer bir deyişle, bir Azure AD kullanıcısının Marketo ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="edd4f-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="edd4f-141">Marketo içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="edd4f-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="edd4f-142">Yapılandırma ve Azure AD çoklu oturum açma Marketo ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="edd4f-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="edd4f-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="edd4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="edd4f-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="edd4f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="edd4f-145">**[Marketo test kullanıcısı oluşturma](#creating-a-marketo-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Marketo sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="edd4f-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="edd4f-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="edd4f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="edd4f-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="edd4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="edd4f-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="edd4f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="edd4f-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Marketo uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="edd4f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="edd4f-150">**Azure AD çoklu oturum açma ile Marketo yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="edd4f-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="edd4f-151">Azure portalında üzerinde **Marketo** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="edd4f-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="edd4f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="edd4f-155">Üzerinde **Marketo etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="edd4f-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="edd4f-157">a.</span><span class="sxs-lookup"><span data-stu-id="edd4f-157">a.</span></span> <span data-ttu-id="edd4f-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="edd4f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="edd4f-159">b.</span><span class="sxs-lookup"><span data-stu-id="edd4f-159">b.</span></span> <span data-ttu-id="edd4f-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="edd4f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="edd4f-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="edd4f-161">These values are not real.</span></span> <span data-ttu-id="edd4f-162">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="edd4f-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="edd4f-163">Kişi [Marketo destek ekibi](http://investors.marketo.com/contactus.cfm) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="edd4f-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
4. <span data-ttu-id="edd4f-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="edd4f-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="edd4f-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="edd4f-168">Üzerinde **Marketo yapılandırma** 'yi tıklatın **yapılandırma Marketo** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="edd4f-169">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="edd4f-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="edd4f-171">Uygulamanızı Munchkin kimliğini almak için Marketo için yönetici kimlik bilgilerinizi kullanarak oturum açın ve aşağıdaki işlemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="edd4f-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="edd4f-172">a.</span><span class="sxs-lookup"><span data-stu-id="edd4f-172">a.</span></span> <span data-ttu-id="edd4f-173">Marketo uygulamasına yönetici kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="edd4f-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="edd4f-174">b.</span><span class="sxs-lookup"><span data-stu-id="edd4f-174">b.</span></span> <span data-ttu-id="edd4f-175">Tıklatın **yönetici** üst gezinti bölmesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="edd4f-177">c.</span><span class="sxs-lookup"><span data-stu-id="edd4f-177">c.</span></span> <span data-ttu-id="edd4f-178">Tümleştirme menüsüne gidin ve tıklayın **Munchkin bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="edd4f-180">d.</span><span class="sxs-lookup"><span data-stu-id="edd4f-180">d.</span></span> <span data-ttu-id="edd4f-181">Ekranda gösterilen Munchkin kimliğini kopyalayın ve yanıt URL'nizi Azure AD Yapılandırma Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="edd4f-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="edd4f-183">Uygulamada SSO yapılandırmak için izleyin aşağıdaki adımları:</span><span class="sxs-lookup"><span data-stu-id="edd4f-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="edd4f-184">a.</span><span class="sxs-lookup"><span data-stu-id="edd4f-184">a.</span></span> <span data-ttu-id="edd4f-185">Marketo uygulamasına yönetici kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="edd4f-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="edd4f-186">b.</span><span class="sxs-lookup"><span data-stu-id="edd4f-186">b.</span></span> <span data-ttu-id="edd4f-187">Tıklatın **yönetici** üst gezinti bölmesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="edd4f-189">c.</span><span class="sxs-lookup"><span data-stu-id="edd4f-189">c.</span></span> <span data-ttu-id="edd4f-190">Tümleştirme menüsüne gidin ve tıklayın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="edd4f-192">d.</span><span class="sxs-lookup"><span data-stu-id="edd4f-192">d.</span></span> <span data-ttu-id="edd4f-193">SAML ayarlarını etkinleştirmek için **Düzenle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="edd4f-195">e.</span><span class="sxs-lookup"><span data-stu-id="edd4f-195">e.</span></span> <span data-ttu-id="edd4f-196">**Etkin** çoklu oturum açma ayarları.</span><span class="sxs-lookup"><span data-stu-id="edd4f-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="edd4f-197">f.</span><span class="sxs-lookup"><span data-stu-id="edd4f-197">f.</span></span> <span data-ttu-id="edd4f-198">Yapıştır **SAML varlık kimliği**, **verenin kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="edd4f-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="edd4f-199">g.</span><span class="sxs-lookup"><span data-stu-id="edd4f-199">g.</span></span> <span data-ttu-id="edd4f-200">İçinde **varlık kimliği** metin kutusuna, URL olarak girin `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="edd4f-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="edd4f-201">h.</span><span class="sxs-lookup"><span data-stu-id="edd4f-201">h.</span></span> <span data-ttu-id="edd4f-202">Kullanıcı Kimliği konum olarak seçin **adı tanımlayıcı öğe**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="edd4f-204">Kullanıcı tanımlayıcısı UPN değeri sonra değişiklik özniteliği sekmesini değerinde değilse.</span><span class="sxs-lookup"><span data-stu-id="edd4f-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="edd4f-205">ı.</span><span class="sxs-lookup"><span data-stu-id="edd4f-205">i.</span></span> <span data-ttu-id="edd4f-206">Azure AD Yapılandırma Sihirbazı'ndan indirilen sertifikasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="edd4f-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="edd4f-207">**Kaydet** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edd4f-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="edd4f-208">j.</span><span class="sxs-lookup"><span data-stu-id="edd4f-208">j.</span></span> <span data-ttu-id="edd4f-209">Yeniden yönlendirme sayfası ayarlarını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="edd4f-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="edd4f-210">k.</span><span class="sxs-lookup"><span data-stu-id="edd4f-210">k.</span></span> <span data-ttu-id="edd4f-211">Yapıştır **SAML çoklu oturum açma hizmet URL'si** içinde **oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="edd4f-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="edd4f-212">l.</span><span class="sxs-lookup"><span data-stu-id="edd4f-212">l.</span></span> <span data-ttu-id="edd4f-213">Yapıştır **Sign-Out URL** içinde **oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="edd4f-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="edd4f-214">m.</span><span class="sxs-lookup"><span data-stu-id="edd4f-214">m.</span></span> <span data-ttu-id="edd4f-215">İçinde **hata URL**, kopyalama, **Marketo örnek URL'si** tıklatıp **kaydetmek** ayarlarını kaydetmek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="edd4f-217">Kullanıcılar için SSO'yu etkinleştirmek için aşağıdaki eylemleri tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="edd4f-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="edd4f-218">a.</span><span class="sxs-lookup"><span data-stu-id="edd4f-218">a.</span></span> <span data-ttu-id="edd4f-219">Marketo uygulamasına yönetici kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="edd4f-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="edd4f-220">b.</span><span class="sxs-lookup"><span data-stu-id="edd4f-220">b.</span></span> <span data-ttu-id="edd4f-221">Tıklatın **yönetici** üst gezinti bölmesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="edd4f-223">c.</span><span class="sxs-lookup"><span data-stu-id="edd4f-223">c.</span></span> <span data-ttu-id="edd4f-224">Gidin **güvenlik** menüsüne ve ardından **oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="edd4f-226">d.</span><span class="sxs-lookup"><span data-stu-id="edd4f-226">d.</span></span> <span data-ttu-id="edd4f-227">Denetleme **gerektiren SSO** seçeneği ve **kaydetmek** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="edd4f-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="edd4f-229">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="edd4f-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="edd4f-230">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="edd4f-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="edd4f-231">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="edd4f-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="edd4f-232">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="edd4f-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="edd4f-233">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="edd4f-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="edd4f-235">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="edd4f-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="edd4f-236">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="edd4f-238">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="edd4f-240">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="edd4f-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="edd4f-242">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="edd4f-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="edd4f-244">a.</span><span class="sxs-lookup"><span data-stu-id="edd4f-244">a.</span></span> <span data-ttu-id="edd4f-245">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edd4f-246">b.</span><span class="sxs-lookup"><span data-stu-id="edd4f-246">b.</span></span> <span data-ttu-id="edd4f-247">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="edd4f-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="edd4f-248">c.</span><span class="sxs-lookup"><span data-stu-id="edd4f-248">c.</span></span> <span data-ttu-id="edd4f-249">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="edd4f-250">d.</span><span class="sxs-lookup"><span data-stu-id="edd4f-250">d.</span></span> <span data-ttu-id="edd4f-251">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="edd4f-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="edd4f-252">Marketo test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="edd4f-252">Creating a Marketo test user</span></span>

<span data-ttu-id="edd4f-253">Bu bölümde, Marketo içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="edd4f-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="edd4f-254">Marketo platformunda bir kullanıcı oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="edd4f-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="edd4f-255">Marketo uygulamasına yönetici kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="edd4f-255">Log in to Marketo app using admin credentials.</span></span>

2. <span data-ttu-id="edd4f-256">Tıklatın **yönetici** üst gezinti bölmesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="edd4f-258">Gidin **güvenlik** menüsüne ve ardından **kullanıcıları ve rolleri**</span><span class="sxs-lookup"><span data-stu-id="edd4f-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="edd4f-260">Tıklatın **yeni kullanıcı davet** kullanıcılar sekmesinde bağlantı</span><span class="sxs-lookup"><span data-stu-id="edd4f-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="edd4f-262">Yeni kullanıcı davet Sihirbazı'nda aşağıdaki bilgileri girin</span><span class="sxs-lookup"><span data-stu-id="edd4f-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="edd4f-263">a.</span><span class="sxs-lookup"><span data-stu-id="edd4f-263">a.</span></span> <span data-ttu-id="edd4f-264">Kullanıcının girmesi **e-posta** metin kutusuna adresi</span><span class="sxs-lookup"><span data-stu-id="edd4f-264">Enter the user **Email** address in the textbox</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="edd4f-266">b.</span><span class="sxs-lookup"><span data-stu-id="edd4f-266">b.</span></span> <span data-ttu-id="edd4f-267">Girin **ad** metin kutusuna</span><span class="sxs-lookup"><span data-stu-id="edd4f-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="edd4f-268">c.</span><span class="sxs-lookup"><span data-stu-id="edd4f-268">c.</span></span> <span data-ttu-id="edd4f-269">Girin **Soyadı** metin kutusuna</span><span class="sxs-lookup"><span data-stu-id="edd4f-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="edd4f-270">d.</span><span class="sxs-lookup"><span data-stu-id="edd4f-270">d.</span></span> <span data-ttu-id="edd4f-271">**İleri**’ye tıklayın</span><span class="sxs-lookup"><span data-stu-id="edd4f-271">Click **Next**</span></span>

6. <span data-ttu-id="edd4f-272">İçinde **izinleri** sekmesine **userRoles** tıklatıp **sonraki**</span><span class="sxs-lookup"><span data-stu-id="edd4f-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="edd4f-274">Tıklatın **Gönder** Kullanıcı Davet Gönder düğmesi</span><span class="sxs-lookup"><span data-stu-id="edd4f-274">Click the **Send** button to send the user invitation</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="edd4f-276">Kullanıcı e-posta bildirimi alır ve bağlantıya tıklayın ve hesabını etkinleştirmek için parolasını değiştirmek zorundadır.</span><span class="sxs-lookup"><span data-stu-id="edd4f-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="edd4f-277">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="edd4f-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="edd4f-278">Bu bölümde, Britta Marketo için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="edd4f-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="edd4f-280">**Marketo için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="edd4f-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="edd4f-281">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="edd4f-283">Uygulamalar listesinde **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-283">In the applications list, select **Marketo**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="edd4f-285">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="edd4f-285">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="edd4f-287">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="edd4f-287">Click **Add** button.</span></span> <span data-ttu-id="edd4f-288">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="edd4f-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="edd4f-290">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="edd4f-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="edd4f-291">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="edd4f-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="edd4f-292">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="edd4f-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="edd4f-293">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="edd4f-293">Testing single sign-on</span></span>

<span data-ttu-id="edd4f-294">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="edd4f-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="edd4f-295">Erişim paneli Marketo parçasında tıklattığınızda, otomatik olarak Marketo uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="edd4f-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="edd4f-296">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="edd4f-296">Additional resources</span></span>

* [<span data-ttu-id="edd4f-297">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="edd4f-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="edd4f-298">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="edd4f-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

