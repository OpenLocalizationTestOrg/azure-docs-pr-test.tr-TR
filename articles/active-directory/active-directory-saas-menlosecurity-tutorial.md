---
title: "Öğretici: Azure Active Directory Tümleştirme Menlo güvenlik | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory Menlo güvenlik arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="0858c-103">Öğretici: Azure Active Directory Tümleştirme Menlo güvenlik</span><span class="sxs-lookup"><span data-stu-id="0858c-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="0858c-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Menlo güvenlik tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0858c-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0858c-105">Menlo güvenlik Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0858c-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0858c-106">Menlo güvenlik erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0858c-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="0858c-107">Azure AD hesaplarına otomatik olarak Menlo güvenlik (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0858c-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0858c-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0858c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0858c-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="0858c-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="0858c-110">[Uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0858c-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0858c-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0858c-111">Prerequisites</span></span>

<span data-ttu-id="0858c-112">Azure AD Tümleştirmesi ile Menlo güvenliği yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="0858c-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="0858c-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0858c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0858c-114">Bir Menlo güvenlik çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="0858c-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0858c-115">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0858c-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0858c-116">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0858c-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0858c-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0858c-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0858c-118">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0858c-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0858c-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0858c-119">Scenario description</span></span>
<span data-ttu-id="0858c-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0858c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0858c-121">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0858c-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0858c-122">Galeriden Menlo güvenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="0858c-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="0858c-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0858c-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="0858c-124">Galeriden Menlo güvenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="0858c-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="0858c-125">Azure AD Menlo güvenlik tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Menlo güvenlik eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0858c-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0858c-126">**Galeriden Menlo güvenlik eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0858c-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0858c-127">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0858c-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0858c-129">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0858c-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0858c-130">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0858c-130">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0858c-132">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0858c-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0858c-134">Arama kutusuna **Menlo güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="0858c-134">In the search box, type **Menlo Security**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="0858c-136">Sonuçlar panelinde seçin **Menlo güvenlik**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0858c-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0858c-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0858c-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0858c-139">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Menlo "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı güvenliği ile test etme</span><span class="sxs-lookup"><span data-stu-id="0858c-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0858c-140">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Menlo güvenliği bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="0858c-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="0858c-141">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Menlo güvenlik arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0858c-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="0858c-142">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Menlo güvenliği.</span><span class="sxs-lookup"><span data-stu-id="0858c-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="0858c-143">Yapılandırma ve Azure AD çoklu oturum açma Menlo güvenlik ile test etmek için aşağıdaki yapı taşları tamamlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="0858c-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0858c-144">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0858c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0858c-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="0858c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0858c-146">**[Menlo güvenlik test kullanıcısı oluşturma](#creating-a-menlo-security-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Menlo güvenlik sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="0858c-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0858c-147">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0858c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0858c-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0858c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0858c-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0858c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0858c-150">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Menlo güvenlik uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0858c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="0858c-151">**Azure AD çoklu oturum açma ile Menlo güvenliği yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0858c-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="0858c-152">Azure portalında üzerinde **Menlo güvenlik** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0858c-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0858c-154">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0858c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="0858c-156">Üzerinde **Menlo güvenlik etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0858c-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="0858c-158">a.</span><span class="sxs-lookup"><span data-stu-id="0858c-158">a.</span></span> <span data-ttu-id="0858c-159">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="0858c-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="0858c-160">b.</span><span class="sxs-lookup"><span data-stu-id="0858c-160">b.</span></span> <span data-ttu-id="0858c-161">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="0858c-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0858c-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="0858c-162">These values are not the real.</span></span> <span data-ttu-id="0858c-163">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0858c-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0858c-164">Kişi [Menlo güvenlik istemci destek ekibi](https://www.menlosecurity.com/menlo-contact) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="0858c-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="0858c-165">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0858c-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="0858c-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0858c-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0858c-169">Üzerinde **Menlo Güvenlik Yapılandırması** 'yi tıklatın **Menlo Güvenlik Yapılandırması** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="0858c-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0858c-170">Kopya **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="0858c-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="0858c-172">Çoklu oturum açma yapılandırmak için **Menlo güvenlik** tarafı, oturum açma **Menlo güvenlik** yönetici olarak Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="0858c-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="0858c-173">Altında **ayarları** gidin **kimlik doğrulaması** ve aşağıdaki işlemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0858c-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="0858c-175">a.</span><span class="sxs-lookup"><span data-stu-id="0858c-175">a.</span></span> <span data-ttu-id="0858c-176">Onay kutusu değer **SAML kullanarak kullanıcı kimlik doğrulamasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="0858c-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="0858c-177">b.</span><span class="sxs-lookup"><span data-stu-id="0858c-177">b.</span></span> <span data-ttu-id="0858c-178">Seçin **dış erişime izin** için **Evet**.</span><span class="sxs-lookup"><span data-stu-id="0858c-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="0858c-179">c.</span><span class="sxs-lookup"><span data-stu-id="0858c-179">c.</span></span> <span data-ttu-id="0858c-180">Altında **SAML sağlayıcısı**seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0858c-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="0858c-181">d.</span><span class="sxs-lookup"><span data-stu-id="0858c-181">d.</span></span> <span data-ttu-id="0858c-182">**SAML 2.0 Endpoint** : Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0858c-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0858c-183">e.</span><span class="sxs-lookup"><span data-stu-id="0858c-183">e.</span></span> <span data-ttu-id="0858c-184">**Hizmet tanımlayıcısı (veren)** : Yapıştır **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0858c-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0858c-185">f.</span><span class="sxs-lookup"><span data-stu-id="0858c-185">f.</span></span> <span data-ttu-id="0858c-186">**X.509 sertifikası** : açık **sertifika (Base64)** Not Defteri'nde Azure portalından indirdiğiniz ve bu kutuya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0858c-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="0858c-187">g.</span><span class="sxs-lookup"><span data-stu-id="0858c-187">g.</span></span> <span data-ttu-id="0858c-188">Tıklatın **kaydetmek** ayarları kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="0858c-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="0858c-189">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0858c-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0858c-190">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="0858c-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0858c-191">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0858c-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0858c-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0858c-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="0858c-193">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="0858c-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0858c-195">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0858c-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0858c-196">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0858c-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0858c-198">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0858c-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0858c-200">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="0858c-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0858c-202">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0858c-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0858c-204">a.</span><span class="sxs-lookup"><span data-stu-id="0858c-204">a.</span></span> <span data-ttu-id="0858c-205">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0858c-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0858c-206">b.</span><span class="sxs-lookup"><span data-stu-id="0858c-206">b.</span></span> <span data-ttu-id="0858c-207">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0858c-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0858c-208">c.</span><span class="sxs-lookup"><span data-stu-id="0858c-208">c.</span></span> <span data-ttu-id="0858c-209">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0858c-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0858c-210">d.</span><span class="sxs-lookup"><span data-stu-id="0858c-210">d.</span></span> <span data-ttu-id="0858c-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0858c-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="0858c-212">Menlo güvenlik test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0858c-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="0858c-213">Bu bölümde, Menlo güvenlik Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0858c-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="0858c-214">Çalışmak [Menlo güvenlik istemci destek ekibi](https://www.menlosecurity.com/menlo-contact) Menlo güvenlik platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="0858c-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="0858c-215">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0858c-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0858c-216">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0858c-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0858c-217">Bu bölümde, Britta Menlo güvenlik erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0858c-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0858c-219">**Menlo güvenlik Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0858c-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="0858c-220">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0858c-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0858c-222">Uygulamalar listesinde **Menlo güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="0858c-222">In the applications list, select **Menlo Security**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="0858c-224">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0858c-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0858c-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0858c-226">Click **Add** button.</span></span> <span data-ttu-id="0858c-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0858c-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0858c-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0858c-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0858c-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0858c-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0858c-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0858c-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0858c-232">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0858c-232">Testing single sign-on</span></span>

<span data-ttu-id="0858c-233">Bu bölümde, Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="0858c-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="0858c-234">Yeni bir kimlik doğrulama tetiklemek için bir "InPrivate" veya "Incognito" modunda bir tarayıcı penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="0858c-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="0858c-235">Internet Explorer'da, Ctrl + Shift + P kullanın.</span><span class="sxs-lookup"><span data-stu-id="0858c-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="0858c-236">Chrome'Ctrl + Shift + N kullanın.</span><span class="sxs-lookup"><span data-stu-id="0858c-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="0858c-237">Özel tarayıcı penceresinde, korunan bir kaynağa gidin ve Azure AD oturum açma gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0858c-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="0858c-238">Başarılı oturum açma sırasında istenen site için bir yalıtım oturumda ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0858c-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0858c-239">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0858c-239">Additional resources</span></span>

* [<span data-ttu-id="0858c-240">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="0858c-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0858c-241">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0858c-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

