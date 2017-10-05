---
title: "Öğretici: Azure Active Directory Tümleştirme ile HappyFox | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile HappyFox arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 8b5ad750d7849e4037ed7ee93c48b5645c68e799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="68d02-103">Öğretici: Azure Active Directory Tümleştirme HappyFox ile</span><span class="sxs-lookup"><span data-stu-id="68d02-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="68d02-104">Bu öğreticide, Azure Active Directory (Azure AD) ile HappyFox tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="68d02-104">In this tutorial, you learn how to integrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68d02-105">HappyFox Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="68d02-105">Integrating HappyFox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="68d02-106">HappyFox erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="68d02-106">You can control in Azure AD who has access to HappyFox</span></span>
- <span data-ttu-id="68d02-107">Otomatik olarak için HappyFox (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="68d02-107">You can enable your users to automatically get signed-on to HappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68d02-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="68d02-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="68d02-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68d02-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68d02-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="68d02-110">Prerequisites</span></span>

<span data-ttu-id="68d02-111">Azure AD tümleştirme HappyFox ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="68d02-111">To configure Azure AD integration with HappyFox, you need the following items:</span></span>

- <span data-ttu-id="68d02-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="68d02-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68d02-113">Bir HappyFox çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="68d02-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68d02-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="68d02-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68d02-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="68d02-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68d02-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="68d02-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68d02-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68d02-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68d02-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="68d02-118">Scenario description</span></span>
<span data-ttu-id="68d02-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="68d02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68d02-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="68d02-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68d02-121">Galeriden HappyFox ekleme</span><span class="sxs-lookup"><span data-stu-id="68d02-121">Adding HappyFox from the gallery</span></span>
2. <span data-ttu-id="68d02-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="68d02-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-the-gallery"></a><span data-ttu-id="68d02-123">Galeriden HappyFox ekleme</span><span class="sxs-lookup"><span data-stu-id="68d02-123">Adding HappyFox from the gallery</span></span>
<span data-ttu-id="68d02-124">Azure AD HappyFox tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden HappyFox eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="68d02-124">To configure the integration of HappyFox into Azure AD, you need to add HappyFox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="68d02-125">**Galeriden HappyFox eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="68d02-125">**To add HappyFox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="68d02-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="68d02-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68d02-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="68d02-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="68d02-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="68d02-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="68d02-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="68d02-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="68d02-133">Arama kutusuna **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="68d02-133">In the search box, type **HappyFox**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="68d02-135">Sonuçlar panelinde seçin **HappyFox**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="68d02-135">In the results panel, select **HappyFox**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68d02-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="68d02-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68d02-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı HappyFox ile test etme</span><span class="sxs-lookup"><span data-stu-id="68d02-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="68d02-139">Tekli çalışmaya oturum için Azure AD HappyFox karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="68d02-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HappyFox is to a user in Azure AD.</span></span> <span data-ttu-id="68d02-140">Diğer bir deyişle, bir Azure AD kullanıcısının HappyFox ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="68d02-140">In other words, a link relationship between an Azure AD user and the related user in HappyFox needs to be established.</span></span>

<span data-ttu-id="68d02-141">HappyFox içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="68d02-141">In HappyFox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="68d02-142">Yapılandırma ve Azure AD çoklu oturum açma HappyFox ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="68d02-142">To configure and test Azure AD single sign-on with HappyFox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="68d02-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="68d02-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="68d02-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="68d02-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68d02-145">**[HappyFox test kullanıcısı oluşturma](#creating-a-happyfox-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı HappyFox sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="68d02-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - to have a counterpart of Britta Simon in HappyFox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="68d02-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="68d02-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68d02-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="68d02-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68d02-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="68d02-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68d02-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma HappyFox uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="68d02-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="68d02-150">**Azure AD çoklu oturum açma ile HappyFox yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="68d02-150">**To configure Azure AD single sign-on with HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="68d02-151">Azure portalında üzerinde **HappyFox** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="68d02-151">In the Azure portal, on the **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="68d02-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="68d02-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="68d02-155">Üzerinde **HappyFox etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="68d02-155">On the **HappyFox Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="68d02-157">a.</span><span class="sxs-lookup"><span data-stu-id="68d02-157">a.</span></span> <span data-ttu-id="68d02-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="68d02-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="68d02-159">b.</span><span class="sxs-lookup"><span data-stu-id="68d02-159">b.</span></span> <span data-ttu-id="68d02-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="68d02-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="68d02-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="68d02-161">These values are not real.</span></span> <span data-ttu-id="68d02-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="68d02-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="68d02-163">Kişi [HappyFox istemci destek ekibi](https://support.happyfox.com/home) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="68d02-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) to get these values.</span></span> 
 
4. <span data-ttu-id="68d02-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="68d02-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="68d02-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="68d02-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="68d02-168">Üzerinde **HappyFox yapılandırma** 'yi tıklatın **yapılandırma HappyFox** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="68d02-168">On the **HappyFox Configuration** section, click **Configure HappyFox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="68d02-169">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümünde**.</span><span class="sxs-lookup"><span data-stu-id="68d02-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="68d02-171">HappyFox personel portalınızda oturum açma ve gidin **Yönet**, tıklayın **tümleştirmeler** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="68d02-171">Sign on to your HappyFox staff portal and navigate to **Manage**, Click on **Integrations** tab.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="68d02-173">Tümleştirmeler sekmesini tıklatın **yapılandırma** altında **SAML tümleştirme** üzerinde tek oturum ayarlarını açın.</span><span class="sxs-lookup"><span data-stu-id="68d02-173">In the Integrations tab, Click **Configure** under **SAML Integration** to open the Single Sign On Settings.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="68d02-175">SAML yapılandırma bölümü yapıştırma **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız **SSO hedef URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="68d02-175">Inside SAML configuration section, paste the **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="68d02-177">Not Defteri'nde Azure portalından indirdiğiniz sertifikasını açın ve içeriğini yapıştırın **IDP imza** bölümü.</span><span class="sxs-lookup"><span data-stu-id="68d02-177">Open the certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="68d02-179">Tıklatın **Ayarları Kaydet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="68d02-179">Click **Save Settings** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="68d02-181">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="68d02-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="68d02-182">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="68d02-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="68d02-183">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68d02-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68d02-184">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="68d02-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="68d02-185">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="68d02-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="68d02-187">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="68d02-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="68d02-188">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="68d02-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68d02-190">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="68d02-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68d02-192">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="68d02-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68d02-194">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="68d02-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68d02-196">a.</span><span class="sxs-lookup"><span data-stu-id="68d02-196">a.</span></span> <span data-ttu-id="68d02-197">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68d02-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68d02-198">b.</span><span class="sxs-lookup"><span data-stu-id="68d02-198">b.</span></span> <span data-ttu-id="68d02-199">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="68d02-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68d02-200">c.</span><span class="sxs-lookup"><span data-stu-id="68d02-200">c.</span></span> <span data-ttu-id="68d02-201">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="68d02-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="68d02-202">d.</span><span class="sxs-lookup"><span data-stu-id="68d02-202">d.</span></span> <span data-ttu-id="68d02-203">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="68d02-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="68d02-204">HappyFox test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="68d02-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="68d02-205">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar uygulamada otomatik olarak oluşturulduktan sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="68d02-205">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="68d02-206">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="68d02-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="68d02-207">Bu bölümde, Britta HappyFox için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="68d02-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HappyFox.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="68d02-209">**HappyFox için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="68d02-209">**To assign Britta Simon to HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="68d02-210">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="68d02-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="68d02-212">Uygulamalar listesinde **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="68d02-212">In the applications list, select **HappyFox**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="68d02-214">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="68d02-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="68d02-216">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="68d02-216">Click **Add** button.</span></span> <span data-ttu-id="68d02-217">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="68d02-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="68d02-219">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="68d02-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="68d02-220">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="68d02-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68d02-221">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="68d02-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68d02-222">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="68d02-222">Testing single sign-on</span></span>

<span data-ttu-id="68d02-223">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="68d02-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="68d02-224">Erişim paneli HappyFox parçasında tıkladığınızda, oturum açma sayfasına HappyFox uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="68d02-224">When you click the HappyFox tile in the Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="68d02-225">Görmeniz gerekir **'SAML'** oturum açma sayfasındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="68d02-225">You should see the **‘SAML’** button on the sign-in page.</span></span>

    ![Eklentisi](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="68d02-227">Tıklatın **'SAML'** düğmesini HappyFox için Azure AD hesabınızı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="68d02-227">Click the **‘SAML’** button to log in to HappyFox using your Azure AD account.</span></span>

<span data-ttu-id="68d02-228">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="68d02-228">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="68d02-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="68d02-229">Additional resources</span></span>

* [<span data-ttu-id="68d02-230">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="68d02-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68d02-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="68d02-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

