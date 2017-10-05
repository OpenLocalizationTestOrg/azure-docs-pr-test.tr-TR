---
title: "Öğretici: Azure Active Directory Tümleştirme Yazı tahtası öğrenin - Shibboleth ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Yazı tahtası öğrenin - Shibboleth arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 014b0671eb8604235a823c2cf4324a49d94df702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="e1ae6-103">Öğretici: Azure Active Directory Tümleştirme Yazı tahtası öğrenin - Shibboleth ile</span><span class="sxs-lookup"><span data-stu-id="e1ae6-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="e1ae6-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Shibboleth tümleştirmek Yazı tahtası öğrenin - öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1ae6-105">Yazı tahtası öğrenin - Shibboleth Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e1ae6-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e1ae6-106">Yazı tahtası öğrenin - Shibboleth erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1ae6-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="e1ae6-107">Otomatik olarak Yazı tahtası öğrenin - Azure AD hesaplarına sahip (çoklu oturum açma) Shibboleth için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1ae6-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1ae6-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e1ae6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e1ae6-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1ae6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1ae6-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1ae6-110">Prerequisites</span></span>

<span data-ttu-id="e1ae6-111">Azure AD tümleştirme Yazı tahtası öğrenin - Shibboleth, ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1ae6-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span></span>

- <span data-ttu-id="e1ae6-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e1ae6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1ae6-113">Yazı tahtası öğrenin - Shibboleth çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e1ae6-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1ae6-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1ae6-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1ae6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1ae6-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1ae6-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1ae6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1ae6-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e1ae6-118">Scenario description</span></span>
<span data-ttu-id="e1ae6-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1ae6-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e1ae6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1ae6-121">Yazı tahtası öğrenin - Shibboleth galerisinden ekleme</span><span class="sxs-lookup"><span data-stu-id="e1ae6-121">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
2. <span data-ttu-id="e1ae6-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1ae6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-the-gallery"></a><span data-ttu-id="e1ae6-123">Yazı tahtası öğrenin - Shibboleth galerisinden ekleme</span><span class="sxs-lookup"><span data-stu-id="e1ae6-123">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
<span data-ttu-id="e1ae6-124">Yazı tahtası öğrenin - Azure AD'ye Shibboleth tümleştirmesini yapılandırmak için Yazı tahtası öğrenin - galerisinden Shibboleth yönetilen SaaS uygulamaları listesine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e1ae6-125">**Yazı tahtası öğrenin - Galerisi'nden Shibboleth eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1ae6-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e1ae6-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1ae6-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e1ae6-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e1ae6-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e1ae6-133">Arama kutusuna **Yazı tahtası öğrenin - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-133">In the search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="e1ae6-135">Sonuçlar panelinde seçin **Yazı tahtası öğrenin - Shibboleth**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-135">In the results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1ae6-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1ae6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1ae6-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Yazı tahtası öğrenin ile test etme - Shibboleth "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="e1ae6-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e1ae6-139">Çoklu oturum açma çalışmak özelliğini için Azure AD ne karşılık gelen kullanıcı Yazı tahtası öğrenin bilmek ister - Shibboleth bir kullanıcıya Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span></span> <span data-ttu-id="e1ae6-140">Diğer bir deyişle, bir Azure AD kullanıcısının ilgili Yazı tahtası öğrenin - kullanıcı arasında bir bağlantı ilişkisi Shibboleth kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span></span>

<span data-ttu-id="e1ae6-141">Yazı tahtası öğrenin - Shibboleth, değeri atamak **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-141">In Blackboard Learn - Shibboleth, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e1ae6-142">Yapılandırmanız ve Azure AD çoklu oturum açma ile Yazı tahtası öğrenin - test Shibboleth, aşağıdaki yapı taşları tamamlanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1ae6-142">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e1ae6-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e1ae6-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1ae6-145">**[Bir Yazı tahtası öğrenin - Shibboleth test kullanıcısı oluşturma](#creating-a-blackboard-learn---shibboleth-test-user)**  - Britta Simon, karşılık gelen Yazı tahtası öğrenin - kullanıcı Azure AD gösterimini bağlı Shibboleth sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1ae6-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1ae6-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1ae6-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1ae6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1ae6-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma, Yazı tahtası öğrenin içinde - Shibboleth uygulama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="e1ae6-150">**Azure AD çoklu oturum açma Yazı tahtası öğrenin - Shibboleth, ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1ae6-150">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="e1ae6-151">Azure portalında üzerinde **Yazı tahtası öğrenin - Shibboleth** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-151">In the Azure portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e1ae6-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="e1ae6-155">Üzerinde **Yazı tahtası öğrenin - Shibboleth etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1ae6-155">On the **Blackboard Learn - Shibboleth Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="e1ae6-157">a.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-157">a.</span></span> <span data-ttu-id="e1ae6-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="e1ae6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="e1ae6-159">b.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-159">b.</span></span> <span data-ttu-id="e1ae6-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="e1ae6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="e1ae6-161">c.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-161">c.</span></span> <span data-ttu-id="e1ae6-162">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="e1ae6-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="e1ae6-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-163">These values are not real.</span></span> <span data-ttu-id="e1ae6-164">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e1ae6-165">Kişi [Yazı tahtası öğrenin - Shibboleth istemci destek ekibi](https://www.blackboard.com/forms/contact-us_form.aspx) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) to get these values.</span></span> 

4. <span data-ttu-id="e1ae6-166">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="e1ae6-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="e1ae6-170">Üzerinde **Yazı tahtası öğrenin - Shibboleth yapılandırma** 'yi tıklatın **yapılandırma Yazı tahtası öğrenin - Shibboleth** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-170">On the **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e1ae6-171">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e1ae6-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="e1ae6-173">Çoklu oturum açma yapılandırmak için **Yazı tahtası öğrenin - Shibboleth** yan, indirilen göndermek için ihtiyacınız **meta veri XML** ve **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si**  için [Yazı tahtası öğrenin - Shibboleth destek ekibi](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1ae6-173">To configure single sign-on on **Blackboard Learn - Shibboleth** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="e1ae6-174">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e1ae6-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e1ae6-175">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e1ae6-176">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1ae6-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1ae6-177">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ae6-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1ae6-178">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e1ae6-180">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1ae6-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e1ae6-181">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1ae6-183">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1ae6-185">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1ae6-187">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1ae6-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1ae6-189">a.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-189">a.</span></span> <span data-ttu-id="e1ae6-190">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1ae6-191">b.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-191">b.</span></span> <span data-ttu-id="e1ae6-192">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1ae6-193">c.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-193">c.</span></span> <span data-ttu-id="e1ae6-194">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e1ae6-195">d.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-195">d.</span></span> <span data-ttu-id="e1ae6-196">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="e1ae6-197">Bir Yazı tahtası öğrenin - Shibboleth test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ae6-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="e1ae6-198">Bu bölümde, Yazı tahtası öğrenin - Shibboleth içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="e1ae6-199">Çalışmak, [Yazı tahtası öğrenin - Shibboleth destek ekibi](https://www.blackboard.com/forms/contact-us_form.aspx) Yazı tahtası öğrenin içinde - Shibboleth platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) to add the users in the Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e1ae6-200">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e1ae6-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e1ae6-201">Bu bölümde, Britta Yazı tahtası öğrenin - Shibboleth erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn - Shibboleth.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e1ae6-203">**Yazı tahtası öğrenin - Shibboleth, Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1ae6-203">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="e1ae6-204">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e1ae6-206">Uygulamalar listesinde **Yazı tahtası öğrenin - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-206">In the applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="e1ae6-208">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e1ae6-210">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-210">Click **Add** button.</span></span> <span data-ttu-id="e1ae6-211">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e1ae6-213">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e1ae6-214">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1ae6-215">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1ae6-216">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e1ae6-216">Testing single sign-on</span></span>

<span data-ttu-id="e1ae6-217">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e1ae6-218">Yazı tahtası öğrenin - Shibboleth kutucuğu erişim Paneli'nde tıklattığınızda, otomatik olarak, Yazı tahtası öğrenin - Shibboleth uygulama açan.</span><span class="sxs-lookup"><span data-stu-id="e1ae6-218">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1ae6-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e1ae6-219">Additional resources</span></span>

* [<span data-ttu-id="e1ae6-220">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e1ae6-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1ae6-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e1ae6-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

