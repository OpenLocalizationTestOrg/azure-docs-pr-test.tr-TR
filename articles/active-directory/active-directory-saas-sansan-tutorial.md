---
title: "Öğretici: Azure Active Directory Tümleştirme ile Sansan | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Sansan arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e1a9653d5feea910308cefabdbdfe3a6af44bbe4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="ee2e1-103">Öğretici: Azure Active Directory Tümleştirme Sansan ile</span><span class="sxs-lookup"><span data-stu-id="ee2e1-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="ee2e1-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Sansan tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-104">In this tutorial, you learn how to integrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee2e1-105">Sansan Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ee2e1-105">Integrating Sansan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ee2e1-106">Sansan erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ee2e1-106">You can control in Azure AD who has access to Sansan</span></span>
- <span data-ttu-id="ee2e1-107">Otomatik olarak için Sansan (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ee2e1-107">You can enable your users to automatically get signed-on to Sansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee2e1-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ee2e1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ee2e1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ee2e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee2e1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ee2e1-110">Prerequisites</span></span>

<span data-ttu-id="ee2e1-111">Azure AD tümleştirme Sansan ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ee2e1-111">To configure Azure AD integration with Sansan, you need the following items:</span></span>

- <span data-ttu-id="ee2e1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ee2e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee2e1-113">Bir Sansan çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="ee2e1-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee2e1-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee2e1-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ee2e1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee2e1-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee2e1-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee2e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee2e1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ee2e1-118">Scenario description</span></span>
<span data-ttu-id="ee2e1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee2e1-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ee2e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee2e1-121">Galeriden Sansan ekleme</span><span class="sxs-lookup"><span data-stu-id="ee2e1-121">Adding Sansan from the gallery</span></span>
2. <span data-ttu-id="ee2e1-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ee2e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-the-gallery"></a><span data-ttu-id="ee2e1-123">Galeriden Sansan ekleme</span><span class="sxs-lookup"><span data-stu-id="ee2e1-123">Adding Sansan from the gallery</span></span>
<span data-ttu-id="ee2e1-124">Azure AD Sansan tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Sansan eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-124">To configure the integration of Sansan into Azure AD, you need to add Sansan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ee2e1-125">**Galeriden Sansan eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ee2e1-125">**To add Sansan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ee2e1-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ee2e1-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ee2e1-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ee2e1-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ee2e1-133">Arama kutusuna **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-133">In the search box, type **Sansan**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="ee2e1-135">Sonuçlar panelinde seçin **Sansan**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-135">In the results panel, select **Sansan**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee2e1-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ee2e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee2e1-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Sansan sınayın.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ee2e1-139">Tekli çalışmaya oturum için Azure AD Sansan karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sansan is to a user in Azure AD.</span></span> <span data-ttu-id="ee2e1-140">Diğer bir deyişle, bir Azure AD kullanıcısının Sansan ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-140">In other words, a link relationship between an Azure AD user and the related user in Sansan needs to be established.</span></span>

<span data-ttu-id="ee2e1-141">Sansan içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-141">In Sansan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ee2e1-142">Yapılandırma ve Azure AD çoklu oturum açma Sansan ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ee2e1-142">To configure and test Azure AD single sign-on with Sansan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ee2e1-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ee2e1-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee2e1-145">**[Sansan test kullanıcısı oluşturma](#creating-a-sansan-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Sansan sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - to have a counterpart of Britta Simon in Sansan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee2e1-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee2e1-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee2e1-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ee2e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee2e1-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Sansan uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="ee2e1-150">**Azure AD çoklu oturum açma ile Sansan yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ee2e1-150">**To configure Azure AD single sign-on with Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="ee2e1-151">Azure portalında üzerinde **Sansan** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-151">In the Azure portal, on the **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ee2e1-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="ee2e1-155">Üzerinde **Sansan etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ee2e1-155">On the **Sansan Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="ee2e1-157">a.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-157">a.</span></span> <span data-ttu-id="ee2e1-158">İçinde **oturum açma URL'si** metin kutusuna, aşağıdaki desenleri kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="ee2e1-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | <span data-ttu-id="ee2e1-159">Ortam</span><span class="sxs-lookup"><span data-stu-id="ee2e1-159">Environment</span></span> | <span data-ttu-id="ee2e1-160">URL</span><span class="sxs-lookup"><span data-stu-id="ee2e1-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="ee2e1-161">Koruyun web</span><span class="sxs-lookup"><span data-stu-id="ee2e1-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="ee2e1-162">Yerel mobil uygulama</span><span class="sxs-lookup"><span data-stu-id="ee2e1-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="ee2e1-163">Mobil tarayıcı ayarları</span><span class="sxs-lookup"><span data-stu-id="ee2e1-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="ee2e1-164">b.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-164">b.</span></span> <span data-ttu-id="ee2e1-165">İçinde **tanımlayıcısı** metin kutusuna, aşağıdaki desenleri kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="ee2e1-165">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="ee2e1-166">Ortam</span><span class="sxs-lookup"><span data-stu-id="ee2e1-166">Environment</span></span>             | <span data-ttu-id="ee2e1-167">URL</span><span class="sxs-lookup"><span data-stu-id="ee2e1-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="ee2e1-168">Koruyun web</span><span class="sxs-lookup"><span data-stu-id="ee2e1-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="ee2e1-169">Yerel mobil uygulama</span><span class="sxs-lookup"><span data-stu-id="ee2e1-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="ee2e1-170">Mobil tarayıcı ayarları</span><span class="sxs-lookup"><span data-stu-id="ee2e1-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="ee2e1-171">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-171">These values are not real.</span></span> <span data-ttu-id="ee2e1-172">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-172">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ee2e1-173">Kişi [Sansan istemci destek ekibi](https://www.sansan.com/form/contact) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) to get these values.</span></span> 

4. <span data-ttu-id="ee2e1-174">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-174">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="ee2e1-176">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-176">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ee2e1-178">Üzerinde **Sansan yapılandırma** 'yi tıklatın **yapılandırma Sansan** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-178">On the **Sansan Configuration** section, click **Configure Sansan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ee2e1-179">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="ee2e1-179">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="ee2e1-181">Çoklu oturum açma yapılandırmak için **Sansan** yan, indirilen göndermek için ihtiyacınız **sertifika**, **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** için [Sansan destek ekibi](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="ee2e1-181">To configure single sign-on on **Sansan** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="ee2e1-182">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-182">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="ee2e1-183">Bilgisayar Tarayıcı ayarını da iş mobil uygulama ve PC web birlikte mobil tarayıcı için.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="ee2e1-184">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ee2e1-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ee2e1-185">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ee2e1-186">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee2e1-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee2e1-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee2e1-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee2e1-188">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ee2e1-190">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ee2e1-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ee2e1-191">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee2e1-193">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee2e1-195">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee2e1-197">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ee2e1-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee2e1-199">a.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-199">a.</span></span> <span data-ttu-id="ee2e1-200">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee2e1-201">b.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-201">b.</span></span> <span data-ttu-id="ee2e1-202">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee2e1-203">c.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-203">c.</span></span> <span data-ttu-id="ee2e1-204">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ee2e1-205">d.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-205">d.</span></span> <span data-ttu-id="ee2e1-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="ee2e1-207">Sansan test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee2e1-207">Creating a Sansan test user</span></span>

<span data-ttu-id="ee2e1-208">Bu bölümde, SanSan içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="ee2e1-209">SanSan uygulama kullanıcının SSO yapmadan önce uygulamayı sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-209">SanSan application needs the user to be provisioned in the application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="ee2e1-210">Bir kullanıcı el ile oluşturabilir veya toplu gerekiyorsa kullanıcıları, başvurmanız gerekir. [Sansan destek ekibi](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="ee2e1-210">If you need to create a user manually or batch of users, you need to contact the [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ee2e1-211">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ee2e1-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ee2e1-212">Bu bölümde, Britta Sansan için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sansan.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ee2e1-214">**Sansan için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ee2e1-214">**To assign Britta Simon to Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="ee2e1-215">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ee2e1-217">Uygulamalar listesinde **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-217">In the applications list, select **Sansan**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="ee2e1-219">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ee2e1-221">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-221">Click **Add** button.</span></span> <span data-ttu-id="ee2e1-222">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ee2e1-224">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ee2e1-225">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee2e1-226">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee2e1-227">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ee2e1-227">Testing single sign-on</span></span>

<span data-ttu-id="ee2e1-228">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ee2e1-229">Erişim paneli Sansan parçasında tıklattığınızda, otomatik olarak Sansan uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="ee2e1-229">When you click the Sansan tile in the Access Panel, you should get automatically signed-on to your Sansan application.</span></span>
<span data-ttu-id="ee2e1-230">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee2e1-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ee2e1-231">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ee2e1-231">Additional resources</span></span>

* [<span data-ttu-id="ee2e1-232">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="ee2e1-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee2e1-233">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ee2e1-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

