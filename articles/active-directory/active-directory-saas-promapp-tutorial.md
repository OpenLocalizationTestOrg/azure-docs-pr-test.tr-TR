---
title: "Öğretici: Azure Active Directory Tümleştirme ile Promapp | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Promapp arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 27013ca9724cf2f57fc85f5f4ccb71921ca57a3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="f5859-103">Öğretici: Azure Active Directory Tümleştirme Promapp ile</span><span class="sxs-lookup"><span data-stu-id="f5859-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="f5859-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Promapp tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f5859-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5859-105">Promapp Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f5859-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5859-106">Promapp erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f5859-106">You can control in Azure AD who has access to Promapp</span></span>
- <span data-ttu-id="f5859-107">Otomatik olarak için Promapp (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f5859-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5859-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f5859-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f5859-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5859-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5859-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f5859-110">Prerequisites</span></span>

<span data-ttu-id="f5859-111">Azure AD tümleştirme Promapp ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="f5859-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

- <span data-ttu-id="f5859-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f5859-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5859-113">Bir Promapp çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f5859-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5859-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f5859-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5859-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f5859-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5859-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f5859-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5859-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5859-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5859-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f5859-118">Scenario description</span></span>
<span data-ttu-id="f5859-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f5859-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5859-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f5859-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5859-121">Galeriden Promapp ekleme</span><span class="sxs-lookup"><span data-stu-id="f5859-121">Adding Promapp from the gallery</span></span>
2. <span data-ttu-id="f5859-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f5859-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-the-gallery"></a><span data-ttu-id="f5859-123">Galeriden Promapp ekleme</span><span class="sxs-lookup"><span data-stu-id="f5859-123">Adding Promapp from the gallery</span></span>
<span data-ttu-id="f5859-124">Azure AD Promapp tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Promapp eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5859-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5859-125">**Galeriden Promapp eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f5859-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5859-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f5859-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5859-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f5859-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5859-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f5859-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f5859-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f5859-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f5859-133">Arama kutusuna **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="f5859-133">In the search box, type **Promapp**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="f5859-135">Sonuçlar panelinde seçin **Promapp**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f5859-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5859-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f5859-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5859-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Promapp sınayın.</span><span class="sxs-lookup"><span data-stu-id="f5859-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5859-139">Tekli çalışmaya oturum için Azure AD Promapp karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="f5859-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span></span> <span data-ttu-id="f5859-140">Diğer bir deyişle, bir Azure AD kullanıcısının Promapp ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5859-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>

<span data-ttu-id="f5859-141">Promapp içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f5859-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f5859-142">Yapılandırma ve Azure AD çoklu oturum açma Promapp ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f5859-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5859-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f5859-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5859-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="f5859-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5859-145">**[Promapp test kullanıcısı oluşturma](#creating-a-promapp-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Promapp sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="f5859-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5859-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f5859-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5859-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f5859-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5859-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f5859-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5859-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Promapp uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f5859-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="f5859-150">**Azure AD çoklu oturum açma ile Promapp yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f5859-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="f5859-151">Azure portalında üzerinde **Promapp** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f5859-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f5859-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f5859-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="f5859-155">Üzerinde **Promapp etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f5859-155">On the **Promapp Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="f5859-157">a.</span><span class="sxs-lookup"><span data-stu-id="f5859-157">a.</span></span> <span data-ttu-id="f5859-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="f5859-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="f5859-159">b.</span><span class="sxs-lookup"><span data-stu-id="f5859-159">b.</span></span> <span data-ttu-id="f5859-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="f5859-160">In the **Identifier** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5859-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="f5859-161">These values are not real.</span></span> <span data-ttu-id="f5859-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f5859-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f5859-163">Kişi [Promapp istemci destek ekibi](https://www.promapp.com/about-us/contact-us/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="f5859-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="f5859-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f5859-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="f5859-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f5859-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5859-168">Üzerinde **Promapp yapılandırma** 'yi tıklatın **yapılandırma Promapp** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="f5859-168">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f5859-169">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="f5859-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="f5859-171">Promapp şirket sitenize yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="f5859-171">Sign-on to your Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="f5859-172">Üstteki menüde tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="f5859-172">In the menu on the top, click **Admin**.</span></span> 
   
    ![Azure AD çoklu oturum açma][12]

9. <span data-ttu-id="f5859-174">**Yapılandır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5859-174">Click **Configure**.</span></span> 
   
    ![Azure AD çoklu oturum açma][13]

10. <span data-ttu-id="f5859-176">Üzerinde **güvenlik** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f5859-176">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Azure AD çoklu oturum açma][14]
    
    <span data-ttu-id="f5859-178">a.</span><span class="sxs-lookup"><span data-stu-id="f5859-178">a.</span></span> <span data-ttu-id="f5859-179">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan **SSO oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f5859-179">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="f5859-180">b.</span><span class="sxs-lookup"><span data-stu-id="f5859-180">b.</span></span> <span data-ttu-id="f5859-181">Olarak **SSO - çoklu oturum açma modu**seçin **isteğe bağlı**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f5859-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="f5859-182">c.</span><span class="sxs-lookup"><span data-stu-id="f5859-182">c.</span></span> <span data-ttu-id="f5859-183">Açık indirilen sertifikayı Not Defteri'nde, kopyalamak sertifika içeriğini yapıştırın (---Başlangıç sertifika---) ilk satırın ve son satır (---son SERTİFİKAYI---) olmadan içine **SSO x.509 sertifikası** metin kutusuna ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f5859-183">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----BEGIN CERTIFICATE-----) and the last line (-----END CERTIFICATE-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="f5859-184">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f5859-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f5859-185">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="f5859-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f5859-186">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f5859-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5859-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5859-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5859-188">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="f5859-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f5859-190">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f5859-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5859-191">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f5859-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5859-193">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f5859-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5859-195">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="f5859-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5859-197">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f5859-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5859-199">a.</span><span class="sxs-lookup"><span data-stu-id="f5859-199">a.</span></span> <span data-ttu-id="f5859-200">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5859-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5859-201">b.</span><span class="sxs-lookup"><span data-stu-id="f5859-201">b.</span></span> <span data-ttu-id="f5859-202">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f5859-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5859-203">c.</span><span class="sxs-lookup"><span data-stu-id="f5859-203">c.</span></span> <span data-ttu-id="f5859-204">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f5859-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f5859-205">d.</span><span class="sxs-lookup"><span data-stu-id="f5859-205">d.</span></span> <span data-ttu-id="f5859-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5859-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="f5859-207">Promapp test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5859-207">Creating a Promapp test user</span></span>

<span data-ttu-id="f5859-208">Zaman içinde sadece Promapp uygulamasının desteklediği sağlama.</span><span class="sxs-lookup"><span data-stu-id="f5859-208">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="f5859-209">Bunun anlamı bir kullanıcı hesabı otomatik olarak gerekirse erişim paneli kullanarak uygulamayı erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f5859-209">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f5859-210">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f5859-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f5859-211">Bu bölümde, Britta Promapp için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f5859-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f5859-213">**Promapp için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f5859-213">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="f5859-214">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f5859-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f5859-216">Uygulamalar listesinde **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="f5859-216">In the applications list, select **Promapp**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="f5859-218">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f5859-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f5859-220">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f5859-220">Click **Add** button.</span></span> <span data-ttu-id="f5859-221">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f5859-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f5859-223">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f5859-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f5859-224">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f5859-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5859-225">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f5859-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5859-226">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f5859-226">Testing single sign-on</span></span>

<span data-ttu-id="f5859-227">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="f5859-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f5859-228">Erişim paneli Promapp parçasında tıklattığınızda, otomatik olarak Promapp uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="f5859-228">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5859-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f5859-229">Additional resources</span></span>

* [<span data-ttu-id="f5859-230">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="f5859-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5859-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f5859-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

