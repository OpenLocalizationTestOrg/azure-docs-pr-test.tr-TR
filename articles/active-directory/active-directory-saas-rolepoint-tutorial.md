---
title: "Öğretici: Azure Active Directory Tümleştirme ile RolePoint | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile RolePoint arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: fcde562484f4401e9f936614b9978f839f4aa290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="ba4a3-103">Öğretici: Azure Active Directory Tümleştirme RolePoint ile</span><span class="sxs-lookup"><span data-stu-id="ba4a3-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="ba4a3-104">Bu öğreticide, Azure Active Directory (Azure AD) ile RolePoint tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-104">In this tutorial, you learn how to integrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba4a3-105">RolePoint Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ba4a3-105">Integrating RolePoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ba4a3-106">RolePoint erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ba4a3-106">You can control in Azure AD who has access to RolePoint</span></span>
- <span data-ttu-id="ba4a3-107">Otomatik olarak için RolePoint (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ba4a3-107">You can enable your users to automatically get signed-on to RolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba4a3-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="ba4a3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ba4a3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba4a3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba4a3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ba4a3-110">Prerequisites</span></span>

<span data-ttu-id="ba4a3-111">Azure AD tümleştirme RolePoint ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="ba4a3-111">To configure Azure AD integration with RolePoint, you need the following items:</span></span>

- <span data-ttu-id="ba4a3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ba4a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba4a3-113">Bir RolePoint çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="ba4a3-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba4a3-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba4a3-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ba4a3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba4a3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba4a3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba4a3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba4a3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ba4a3-118">Scenario description</span></span>
<span data-ttu-id="ba4a3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba4a3-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ba4a3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba4a3-121">Galeriden RolePoint ekleme</span><span class="sxs-lookup"><span data-stu-id="ba4a3-121">Adding RolePoint from the gallery</span></span>
2. <span data-ttu-id="ba4a3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ba4a3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-the-gallery"></a><span data-ttu-id="ba4a3-123">Galeriden RolePoint ekleme</span><span class="sxs-lookup"><span data-stu-id="ba4a3-123">Adding RolePoint from the gallery</span></span>
<span data-ttu-id="ba4a3-124">Azure AD RolePoint tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden RolePoint eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-124">To configure the integration of RolePoint into Azure AD, you need to add RolePoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ba4a3-125">**Galeriden RolePoint eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ba4a3-125">**To add RolePoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ba4a3-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ba4a3-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ba4a3-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ba4a3-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ba4a3-133">Arama kutusuna **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-133">In the search box, type **RolePoint**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="ba4a3-135">Sonuçlar panelinde seçin **RolePoint**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-135">In the results panel, select **RolePoint**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ba4a3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ba4a3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ba4a3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı RolePoint ile test etme</span><span class="sxs-lookup"><span data-stu-id="ba4a3-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ba4a3-139">Tekli çalışmaya oturum için Azure AD RolePoint karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RolePoint is to a user in Azure AD.</span></span> <span data-ttu-id="ba4a3-140">Diğer bir deyişle, bir Azure AD kullanıcısının RolePoint ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-140">In other words, a link relationship between an Azure AD user and the related user in RolePoint needs to be established.</span></span>

<span data-ttu-id="ba4a3-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** RolePoint içinde.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RolePoint.</span></span>

<span data-ttu-id="ba4a3-142">Yapılandırma ve Azure AD çoklu oturum açma RolePoint ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ba4a3-142">To configure and test Azure AD single sign-on with RolePoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ba4a3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ba4a3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba4a3-145">**[RolePoint test kullanıcısı oluşturma](#creating-a-rolepoint-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı RolePoint sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - to have a counterpart of Britta Simon in RolePoint that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba4a3-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba4a3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ba4a3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ba4a3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ba4a3-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma RolePoint uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="ba4a3-150">**Azure AD çoklu oturum açma ile RolePoint yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ba4a3-150">**To configure Azure AD single sign-on with RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="ba4a3-151">Azure portalında üzerinde **RolePoint** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-151">In the Azure portal, on the **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ba4a3-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="ba4a3-155">Üzerinde **RolePoint etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ba4a3-155">On the **RolePoint Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="ba4a3-157">a.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-157">a.</span></span> <span data-ttu-id="ba4a3-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="ba4a3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="ba4a3-159">b.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-159">b.</span></span> <span data-ttu-id="ba4a3-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ba4a3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ba4a3-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-161">These values are not the real.</span></span> <span data-ttu-id="ba4a3-162">Bu değerleri tanımlayıcısı ve gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="ba4a3-163">Dizenin benzersiz değer Identifier.Contact kullanmanızı öneririz burada [RolePoint destek ekibi](mailto:info@rolepoint.com) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-163">Here we suggest you to use the unique value of string in the Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) to get the value.</span></span> 
 
4. <span data-ttu-id="ba4a3-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="ba4a3-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="ba4a3-168">Çoklu oturum açma yapılandırmak için **RolePoint** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [RolePoint destek ekibi](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="ba4a3-168">To configure single sign-on on **RolePoint** side, you need to send the downloaded **Metadata XML** to [RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="ba4a3-169">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ba4a3-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ba4a3-170">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ba4a3-171">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba4a3-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ba4a3-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba4a3-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="ba4a3-173">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ba4a3-175">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ba4a3-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ba4a3-176">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba4a3-178">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba4a3-180">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba4a3-182">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ba4a3-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba4a3-184">a.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-184">a.</span></span> <span data-ttu-id="ba4a3-185">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba4a3-186">b.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-186">b.</span></span> <span data-ttu-id="ba4a3-187">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba4a3-188">c.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-188">c.</span></span> <span data-ttu-id="ba4a3-189">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ba4a3-190">d.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-190">d.</span></span> <span data-ttu-id="ba4a3-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="ba4a3-192">RolePoint test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba4a3-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="ba4a3-193">Bu bölümde, RolePoint içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="ba4a3-194">Çalışmak [RolePoint destek ekibi](mailto:info@rolepoint.com) RolePoint platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-194">Work with [RolePoint support team](mailto:info@rolepoint.com) to add the users in the RolePoint platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ba4a3-195">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ba4a3-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ba4a3-196">Bu bölümde, Britta RolePoint için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RolePoint.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ba4a3-198">**RolePoint için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ba4a3-198">**To assign Britta Simon to RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="ba4a3-199">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ba4a3-201">Uygulamalar listesinde **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-201">In the applications list, select **RolePoint**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="ba4a3-203">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ba4a3-205">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-205">Click **Add** button.</span></span> <span data-ttu-id="ba4a3-206">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ba4a3-208">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ba4a3-209">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba4a3-210">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ba4a3-211">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ba4a3-211">Testing single sign-on</span></span>

<span data-ttu-id="ba4a3-212">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ba4a3-213">Erişim paneli RolePoint parçasında tıklattığınızda, otomatik olarak RolePoint uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="ba4a3-213">When you click the RolePoint tile in the Access Panel, you should get automatically signed-on to your RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ba4a3-214">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ba4a3-214">Additional resources</span></span>

* [<span data-ttu-id="ba4a3-215">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="ba4a3-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba4a3-216">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ba4a3-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

