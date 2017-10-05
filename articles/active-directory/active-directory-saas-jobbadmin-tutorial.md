---
title: "Öğretici: Azure Active Directory Tümleştirme ile Jobbadmin | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Jobbadmin arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c5208b0d-66a3-49ed-9aad-70d21f54aee0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 848a6d6d0f072bc3f697ff57756714fc45e7dcc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobbadmin"></a><span data-ttu-id="b6b86-103">Öğretici: Azure Active Directory Tümleştirme Jobbadmin ile</span><span class="sxs-lookup"><span data-stu-id="b6b86-103">Tutorial: Azure Active Directory integration with Jobbadmin</span></span>

<span data-ttu-id="b6b86-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Jobbadmin tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b6b86-104">In this tutorial, you learn how to integrate Jobbadmin with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6b86-105">Jobbadmin Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b6b86-105">Integrating Jobbadmin with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b6b86-106">Jobbadmin erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b6b86-106">You can control in Azure AD who has access to Jobbadmin</span></span>
- <span data-ttu-id="b6b86-107">Otomatik olarak için Jobbadmin (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b6b86-107">You can enable your users to automatically get signed-on to Jobbadmin (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6b86-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b6b86-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b6b86-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6b86-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6b86-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b6b86-110">Prerequisites</span></span>

<span data-ttu-id="b6b86-111">Azure AD tümleştirme Jobbadmin ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="b6b86-111">To configure Azure AD integration with Jobbadmin, you need the following items:</span></span>

- <span data-ttu-id="b6b86-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b6b86-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6b86-113">Bir Jobbadmin çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="b6b86-113">A Jobbadmin single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6b86-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b6b86-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6b86-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b6b86-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6b86-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b6b86-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6b86-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6b86-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6b86-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b6b86-118">Scenario description</span></span>
<span data-ttu-id="b6b86-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b6b86-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6b86-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b6b86-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6b86-121">Galeriden Jobbadmin ekleme</span><span class="sxs-lookup"><span data-stu-id="b6b86-121">Adding Jobbadmin from the gallery</span></span>
2. <span data-ttu-id="b6b86-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b6b86-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobbadmin-from-the-gallery"></a><span data-ttu-id="b6b86-123">Galeriden Jobbadmin ekleme</span><span class="sxs-lookup"><span data-stu-id="b6b86-123">Adding Jobbadmin from the gallery</span></span>
<span data-ttu-id="b6b86-124">Azure AD Jobbadmin tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Jobbadmin eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6b86-124">To configure the integration of Jobbadmin into Azure AD, you need to add Jobbadmin from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b6b86-125">**Galeriden Jobbadmin eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b6b86-125">**To add Jobbadmin from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b6b86-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b6b86-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b6b86-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b6b86-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b6b86-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b6b86-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b6b86-133">Arama kutusuna **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-133">In the search box, type **Jobbadmin**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_search.png)

5. <span data-ttu-id="b6b86-135">Sonuçlar panelinde seçin **Jobbadmin**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b6b86-135">In the results panel, select **Jobbadmin**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b6b86-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b6b86-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b6b86-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Jobbadmin ile test etme</span><span class="sxs-lookup"><span data-stu-id="b6b86-138">In this section, you configure and test Azure AD single sign-on with Jobbadmin based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b6b86-139">Tekli çalışmaya oturum için Azure AD Jobbadmin karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="b6b86-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobbadmin is to a user in Azure AD.</span></span> <span data-ttu-id="b6b86-140">Diğer bir deyişle, bir Azure AD kullanıcısının Jobbadmin ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6b86-140">In other words, a link relationship between an Azure AD user and the related user in Jobbadmin needs to be established.</span></span>

<span data-ttu-id="b6b86-141">Jobbadmin içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="b6b86-141">In Jobbadmin, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b6b86-142">Yapılandırma ve Azure AD çoklu oturum açma Jobbadmin ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b6b86-142">To configure and test Azure AD single sign-on with Jobbadmin, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b6b86-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b6b86-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b6b86-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="b6b86-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6b86-145">**[Jobbadmin test kullanıcısı oluşturma](#creating-a-jobbadmin-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Jobbadmin sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="b6b86-145">**[Creating a Jobbadmin test user](#creating-a-jobbadmin-test-user)** - to have a counterpart of Britta Simon in Jobbadmin that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6b86-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b6b86-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6b86-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b6b86-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b6b86-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6b86-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b6b86-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Jobbadmin uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b6b86-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobbadmin application.</span></span>

<span data-ttu-id="b6b86-150">**Azure AD çoklu oturum açma ile Jobbadmin yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b6b86-150">**To configure Azure AD single sign-on with Jobbadmin, perform the following steps:**</span></span>

1. <span data-ttu-id="b6b86-151">Azure portalında üzerinde **Jobbadmin** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-151">In the Azure portal, on the **Jobbadmin** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b6b86-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b6b86-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_samlbase.png)

3. <span data-ttu-id="b6b86-155">Üzerinde **Jobbadmin etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b6b86-155">On the **Jobbadmin Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_url.png)

    <span data-ttu-id="b6b86-157">a.</span><span class="sxs-lookup"><span data-stu-id="b6b86-157">a.</span></span> <span data-ttu-id="b6b86-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="b6b86-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    <span data-ttu-id="b6b86-159">b.</span><span class="sxs-lookup"><span data-stu-id="b6b86-159">b.</span></span> <span data-ttu-id="b6b86-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<instancename>.jobnorge.no`</span><span class="sxs-lookup"><span data-stu-id="b6b86-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.jobnorge.no`</span></span>

    <span data-ttu-id="b6b86-161">c.</span><span class="sxs-lookup"><span data-stu-id="b6b86-161">c.</span></span> <span data-ttu-id="b6b86-162">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="b6b86-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6b86-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="b6b86-163">These values are not real.</span></span> <span data-ttu-id="b6b86-164">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b6b86-164">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b6b86-165">Kişi [Jobbadmin istemci destek ekibi](https://www.jobbnorge.no/om-oss/kontakt-oss) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="b6b86-165">Contact [Jobbadmin Client support team](https://www.jobbnorge.no/om-oss/kontakt-oss) to get these values.</span></span> 
 


4. <span data-ttu-id="b6b86-166">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b6b86-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_certificate.png) 

5. <span data-ttu-id="b6b86-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b6b86-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b6b86-170">Çoklu oturum açma yapılandırmak için **Jobbadmin** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [Jobbadmin destek ekibi](https://www.jobbnorge.no/om-oss/kontakt-oss).</span><span class="sxs-lookup"><span data-stu-id="b6b86-170">To configure single sign-on on **Jobbadmin** side, you need to send the downloaded **Metadata XML** to [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss).</span></span> <span data-ttu-id="b6b86-171">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b6b86-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b6b86-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b6b86-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b6b86-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="b6b86-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b6b86-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b6b86-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b6b86-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6b86-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="b6b86-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b6b86-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b6b86-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b6b86-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b6b86-179">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b6b86-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6b86-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6b86-183">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="b6b86-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6b86-185">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b6b86-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6b86-187">a.</span><span class="sxs-lookup"><span data-stu-id="b6b86-187">a.</span></span> <span data-ttu-id="b6b86-188">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6b86-189">b.</span><span class="sxs-lookup"><span data-stu-id="b6b86-189">b.</span></span> <span data-ttu-id="b6b86-190">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b6b86-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6b86-191">c.</span><span class="sxs-lookup"><span data-stu-id="b6b86-191">c.</span></span> <span data-ttu-id="b6b86-192">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b6b86-193">d.</span><span class="sxs-lookup"><span data-stu-id="b6b86-193">d.</span></span> <span data-ttu-id="b6b86-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6b86-194">Click **Create**.</span></span>
 
### <a name="creating-a-jobbadmin-test-user"></a><span data-ttu-id="b6b86-195">Jobbadmin test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6b86-195">Creating a Jobbadmin test user</span></span>

<span data-ttu-id="b6b86-196">Azure AD kullanıcıları için Jobbadmin oturum açmak etkinleştirmek için bunların Jobbadmin sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6b86-196">To enable Azure AD users to log in to Jobbadmin, they must be provisioned into Jobbadmin.</span></span>
 
<span data-ttu-id="b6b86-197">Temasa [Jobbadmin destek ekibi](https://www.jobbnorge.no/om-oss/kontakt-oss) kullanıcılara kendi tarafında eklendi.</span><span class="sxs-lookup"><span data-stu-id="b6b86-197">Please contact [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss) to get the users added on their side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b6b86-198">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="b6b86-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b6b86-199">Bu bölümde, Britta Jobbadmin için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b6b86-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobbadmin.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b6b86-201">**Jobbadmin için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b6b86-201">**To assign Britta Simon to Jobbadmin, perform the following steps:**</span></span>

1. <span data-ttu-id="b6b86-202">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b6b86-204">Uygulamalar listesinde **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-204">In the applications list, select **Jobbadmin**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_app.png) 

3. <span data-ttu-id="b6b86-206">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b6b86-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b6b86-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b6b86-208">Click **Add** button.</span></span> <span data-ttu-id="b6b86-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b6b86-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b6b86-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b6b86-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b6b86-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b6b86-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6b86-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b6b86-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b6b86-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b6b86-214">Testing single sign-on</span></span>

<span data-ttu-id="b6b86-215">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="b6b86-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b6b86-216">Erişim paneli Jobbadmin parçasında tıkladığınızda, oturum açma sayfasına Jobbadmin uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6b86-216">When you click the Jobbadmin tile in the Access Panel, you should get login page of Jobbadmin application.</span></span>
<span data-ttu-id="b6b86-217">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6b86-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b6b86-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b6b86-218">Additional resources</span></span>

* [<span data-ttu-id="b6b86-219">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="b6b86-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6b86-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b6b86-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_203.png

