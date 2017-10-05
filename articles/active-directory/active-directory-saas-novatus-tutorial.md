---
title: "Öğretici: Azure Active Directory Tümleştirme ile Novatus | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Novatus arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: ec67e96309a8877e6fb65b30da1501e4f34a9ee4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="81b70-103">Öğretici: Azure Active Directory Tümleştirme Novatus ile</span><span class="sxs-lookup"><span data-stu-id="81b70-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="81b70-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Novatus tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="81b70-104">In this tutorial, you learn how to integrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81b70-105">Novatus Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="81b70-105">Integrating Novatus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81b70-106">Novatus erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="81b70-106">You can control in Azure AD who has access to Novatus</span></span>
- <span data-ttu-id="81b70-107">Otomatik olarak için Novatus (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="81b70-107">You can enable your users to automatically get signed-on to Novatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81b70-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="81b70-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="81b70-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81b70-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81b70-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="81b70-110">Prerequisites</span></span>

<span data-ttu-id="81b70-111">Azure AD tümleştirme Novatus ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="81b70-111">To configure Azure AD integration with Novatus, you need the following items:</span></span>

- <span data-ttu-id="81b70-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="81b70-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81b70-113">Bir Novatus çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="81b70-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81b70-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="81b70-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81b70-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="81b70-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81b70-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="81b70-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81b70-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81b70-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81b70-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="81b70-118">Scenario description</span></span>
<span data-ttu-id="81b70-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="81b70-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81b70-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="81b70-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81b70-121">Galeriden Novatus ekleme</span><span class="sxs-lookup"><span data-stu-id="81b70-121">Adding Novatus from the gallery</span></span>
2. <span data-ttu-id="81b70-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="81b70-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-the-gallery"></a><span data-ttu-id="81b70-123">Galeriden Novatus ekleme</span><span class="sxs-lookup"><span data-stu-id="81b70-123">Adding Novatus from the gallery</span></span>
<span data-ttu-id="81b70-124">Azure AD Novatus tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Novatus eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="81b70-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81b70-125">**Galeriden Novatus eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="81b70-125">**To add Novatus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81b70-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="81b70-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81b70-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="81b70-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81b70-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="81b70-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="81b70-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="81b70-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="81b70-133">Arama kutusuna **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="81b70-133">In the search box, type **Novatus**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="81b70-135">Sonuçlar panelinde seçin **Novatus**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="81b70-135">In the results panel, select **Novatus**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81b70-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="81b70-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81b70-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Novatus sınayın.</span><span class="sxs-lookup"><span data-stu-id="81b70-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81b70-139">Tekli çalışmaya oturum için Azure AD Novatus karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="81b70-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Novatus is to a user in Azure AD.</span></span> <span data-ttu-id="81b70-140">Diğer bir deyişle, bir Azure AD kullanıcısının Novatus ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="81b70-140">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span></span>

<span data-ttu-id="81b70-141">Novatus içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="81b70-141">In Novatus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="81b70-142">Yapılandırma ve Azure AD çoklu oturum açma Novatus ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="81b70-142">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81b70-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="81b70-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81b70-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="81b70-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81b70-145">**[Novatus test kullanıcısı oluşturma](#creating-a-novatus-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Novatus sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="81b70-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81b70-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="81b70-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81b70-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="81b70-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81b70-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="81b70-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81b70-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Novatus uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="81b70-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="81b70-150">**Azure AD çoklu oturum açma ile Novatus yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="81b70-150">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="81b70-151">Azure portalında üzerinde **Novatus** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="81b70-151">In the Azure portal, on the **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="81b70-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="81b70-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="81b70-155">Üzerinde **Novatus etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="81b70-155">On the **Novatus Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="81b70-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="81b70-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81b70-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="81b70-158">This value is not real.</span></span> <span data-ttu-id="81b70-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="81b70-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="81b70-160">Kişi [Novatus istemci destek ekibi](mailto:jvinci@novatusinc.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="81b70-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) to get this value.</span></span> 
 


4. <span data-ttu-id="81b70-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="81b70-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="81b70-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="81b70-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81b70-165">Üzerinde **Novatus yapılandırma** 'yi tıklatın **yapılandırma Novatus** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="81b70-165">On the **Novatus Configuration** section, click **Configure Novatus** to open **Configure sign-on** window.</span></span> <span data-ttu-id="81b70-166">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="81b70-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="81b70-168">Uygulamanız için yapılandırılmış SSO almak için başvurun, [Novatus destek ekibi](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="81b70-168">To get SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="81b70-169">Attach **sertifika indirilen** posta ve paylaşımı için dosya **meta verileri URL'leri** (**Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si**) Novatus ile kendi tarafında SSO'yu ayarlamak için takım.</span><span class="sxs-lookup"><span data-stu-id="81b70-169">Attach the **downloaded certificate** file to your mail and share the **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team to set up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="81b70-170">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="81b70-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81b70-171">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="81b70-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81b70-172">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81b70-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81b70-173">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="81b70-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="81b70-174">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="81b70-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="81b70-176">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="81b70-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81b70-177">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="81b70-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81b70-179">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="81b70-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81b70-181">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="81b70-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81b70-183">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="81b70-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81b70-185">a.</span><span class="sxs-lookup"><span data-stu-id="81b70-185">a.</span></span> <span data-ttu-id="81b70-186">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81b70-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81b70-187">b.</span><span class="sxs-lookup"><span data-stu-id="81b70-187">b.</span></span> <span data-ttu-id="81b70-188">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="81b70-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81b70-189">c.</span><span class="sxs-lookup"><span data-stu-id="81b70-189">c.</span></span> <span data-ttu-id="81b70-190">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="81b70-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="81b70-191">d.</span><span class="sxs-lookup"><span data-stu-id="81b70-191">d.</span></span> <span data-ttu-id="81b70-192">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81b70-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="81b70-193">Novatus test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="81b70-193">Creating a Novatus test user</span></span>

<span data-ttu-id="81b70-194">Bu bölümün amacı Britta Simon içinde Novatus adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="81b70-194">The objective of this section is to create a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="81b70-195">Novatus yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="81b70-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="81b70-196">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="81b70-196">There is no action item for you in this section.</span></span> <span data-ttu-id="81b70-197">Yeni bir kullanıcı henüz yoksa Novatus erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="81b70-197">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="81b70-198">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [Novatus destek ekibi](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="81b70-198">If you need to create an user manually, you need to contact the [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="81b70-199">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="81b70-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="81b70-200">Bu bölümde, Britta Novatus için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="81b70-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Novatus.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="81b70-202">**Novatus için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="81b70-202">**To assign Britta Simon to Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="81b70-203">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="81b70-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="81b70-205">Uygulamalar listesinde **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="81b70-205">In the applications list, select **Novatus**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="81b70-207">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="81b70-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="81b70-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="81b70-209">Click **Add** button.</span></span> <span data-ttu-id="81b70-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="81b70-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="81b70-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="81b70-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81b70-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="81b70-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81b70-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="81b70-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81b70-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="81b70-215">Testing single sign-on</span></span>

<span data-ttu-id="81b70-216">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="81b70-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="81b70-217">Erişim paneli Novatus parçasında tıklattığınızda, otomatik olarak Novatus uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="81b70-217">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span></span> <span data-ttu-id="81b70-218">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81b70-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81b70-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="81b70-219">Additional resources</span></span>

* [<span data-ttu-id="81b70-220">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="81b70-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81b70-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="81b70-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

