---
title: "Öğretici: Azure Active Directory Tümleştirme 10.000 ft planına sahip | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile 10.000 ft planları arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: c81a6adb3abad58af149bbef6f5dff736c142f51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="7cb92-103">Öğretici: Azure Active Directory Tümleştirme 10.000 ft planına sahip</span><span class="sxs-lookup"><span data-stu-id="7cb92-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="7cb92-104">Bu öğreticide, Azure Active Directory (Azure AD) ile 10.000 ft planlarının tümleştirmenize öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7cb92-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7cb92-105">10.000 ft planları Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7cb92-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7cb92-106">10.000 ft planları erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7cb92-106">You can control in Azure AD who has access to 10,000ft Plans</span></span>
- <span data-ttu-id="7cb92-107">Otomatik olarak 10.000 ft planlara (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7cb92-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7cb92-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7cb92-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7cb92-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7cb92-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cb92-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7cb92-110">Prerequisites</span></span>

<span data-ttu-id="7cb92-111">Azure AD tümleştirme 10.000 ft planlarıyla yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="7cb92-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span></span>

- <span data-ttu-id="7cb92-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7cb92-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7cb92-113">Bir 10.000 ft planları çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7cb92-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7cb92-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7cb92-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7cb92-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7cb92-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7cb92-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7cb92-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7cb92-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme alabilirsiniz [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7cb92-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7cb92-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7cb92-118">Scenario description</span></span>
<span data-ttu-id="7cb92-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7cb92-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7cb92-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7cb92-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7cb92-121">Galeriden planları 10.000 ft ekleme</span><span class="sxs-lookup"><span data-stu-id="7cb92-121">Adding 10,000ft Plans from the gallery</span></span>
2. <span data-ttu-id="7cb92-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7cb92-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-the-gallery"></a><span data-ttu-id="7cb92-123">Galeriden planları 10.000 ft ekleme</span><span class="sxs-lookup"><span data-stu-id="7cb92-123">Adding 10,000ft Plans from the gallery</span></span>
<span data-ttu-id="7cb92-124">Azure AD 10.000 ft planları tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden 10.000 ft planları eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7cb92-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7cb92-125">**Galeriden 10.000 ft planları eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7cb92-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7cb92-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7cb92-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7cb92-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7cb92-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7cb92-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7cb92-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7cb92-133">Arama kutusuna **10.000 ft planları**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-133">In the search box, type **10,000ft Plans**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="7cb92-135">Sonuçlar panelinde seçin **10.000 ft planları**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7cb92-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7cb92-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7cb92-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7cb92-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma 10.000 ft "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı planları ile test etme</span><span class="sxs-lookup"><span data-stu-id="7cb92-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7cb92-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen 10.000 ft planlarda bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="7cb92-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span></span> <span data-ttu-id="7cb92-140">Diğer bir deyişle, bir Azure AD kullanıcısının 10.000 ft ilgili kullanıcı arasında bir bağlantı ilişkisi planları gerekiyor kurulamıyor.</span><span class="sxs-lookup"><span data-stu-id="7cb92-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span></span>

<span data-ttu-id="7cb92-141">10.000 ft planlarda değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7cb92-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7cb92-142">Yapılandırma ve Azure AD çoklu oturum açma 10.000 ft planları ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7cb92-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7cb92-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7cb92-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7cb92-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="7cb92-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7cb92-145">**[Kullanıcı test planları 10.000 ft oluşturma](#creating-a-10000ft-plans-test-user)**  - bir Britta Simon karşılık gelen kullanıcı Azure AD gösterimini bağlı 10.000 ft planları içinde olması.</span><span class="sxs-lookup"><span data-stu-id="7cb92-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7cb92-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7cb92-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7cb92-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7cb92-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7cb92-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7cb92-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7cb92-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma 10.000 ft planları uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7cb92-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="7cb92-150">**Azure AD çoklu oturum açma 10.000 ft planlarıyla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7cb92-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="7cb92-151">Azure portalında üzerinde **10.000 ft planları** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7cb92-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="7cb92-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="7cb92-155">Üzerinde **10.000 ft planları etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7cb92-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="7cb92-157">a.</span><span class="sxs-lookup"><span data-stu-id="7cb92-157">a.</span></span> <span data-ttu-id="7cb92-158">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="7cb92-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="7cb92-159">b.</span><span class="sxs-lookup"><span data-stu-id="7cb92-159">b.</span></span> <span data-ttu-id="7cb92-160">İçinde **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="7cb92-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7cb92-161">Değeri **tanımlayıcısı** özel bir etki alanı varsa farklıdır.</span><span class="sxs-lookup"><span data-stu-id="7cb92-161">The value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="7cb92-162">Kişi [10.000 ft planları destek ekibi](https://www.10000ft.com/plans/support) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="7cb92-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span></span> 
 
4. <span data-ttu-id="7cb92-163">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Raw)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7cb92-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="7cb92-165">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7cb92-165">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7cb92-167">Üzerinde **10.000 ft planları yapılandırma** 'yi tıklatın **yapılandırma 10.000 ft planları** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7cb92-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7cb92-168">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="7cb92-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="7cb92-170">Çoklu oturum açma yapılandırmak için **10.000 ft planları** yan, indirilen göndermek için ihtiyacınız **Certificate(Raw), Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** için [10.000 ft Planları destek ekibi](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="7cb92-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="7cb92-171">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7cb92-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7cb92-172">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="7cb92-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7cb92-173">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7cb92-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7cb92-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7cb92-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="7cb92-175">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="7cb92-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7cb92-177">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7cb92-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7cb92-178">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7cb92-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7cb92-180">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7cb92-182">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="7cb92-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7cb92-184">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7cb92-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7cb92-186">a.</span><span class="sxs-lookup"><span data-stu-id="7cb92-186">a.</span></span> <span data-ttu-id="7cb92-187">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7cb92-188">b.</span><span class="sxs-lookup"><span data-stu-id="7cb92-188">b.</span></span> <span data-ttu-id="7cb92-189">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7cb92-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7cb92-190">c.</span><span class="sxs-lookup"><span data-stu-id="7cb92-190">c.</span></span> <span data-ttu-id="7cb92-191">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7cb92-192">d.</span><span class="sxs-lookup"><span data-stu-id="7cb92-192">d.</span></span> <span data-ttu-id="7cb92-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7cb92-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="7cb92-194">Kullanıcı test planları 10.000 ft oluşturma</span><span class="sxs-lookup"><span data-stu-id="7cb92-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="7cb92-195">Bu bölümün amacı Britta Simon 10.000 ft planlarda adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="7cb92-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="7cb92-196">10.000 ft planları yalnızca zaman kaynak sağlamayı destekler, varsayılan olarak etkin olduğu.</span><span class="sxs-lookup"><span data-stu-id="7cb92-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="7cb92-197">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="7cb92-197">There is no action item for you in this section.</span></span> <span data-ttu-id="7cb92-198">Yeni bir kullanıcı henüz yoksa 10.000 ft planları erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7cb92-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="7cb92-199">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [10.000 ft planları destek ekibi](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="7cb92-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7cb92-200">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7cb92-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7cb92-201">Bu bölümde, Britta 10.000 ft planlarına erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7cb92-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7cb92-203">**10.000 ft planlarına Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7cb92-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="7cb92-204">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7cb92-206">Uygulamalar listesinde **10.000 ft planları**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-206">In the applications list, select **10,000ft Plans**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="7cb92-208">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7cb92-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7cb92-210">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7cb92-210">Click **Add** button.</span></span> <span data-ttu-id="7cb92-211">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7cb92-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7cb92-213">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7cb92-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7cb92-214">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7cb92-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7cb92-215">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7cb92-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7cb92-216">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7cb92-216">Testing single sign-on</span></span>

<span data-ttu-id="7cb92-217">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="7cb92-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="7cb92-218">Erişim paneli 10.000 ft planları parçasında tıklattığınızda, otomatik olarak 10.000 ft planları uygulamanızı açan.</span><span class="sxs-lookup"><span data-stu-id="7cb92-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="7cb92-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7cb92-219">Additional resources</span></span>

* [<span data-ttu-id="7cb92-220">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="7cb92-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7cb92-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7cb92-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

