---
title: "Öğretici: Azure Active Directory Tümleştirme ile Convercent | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Convercent arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 7af33cae7448a212734d327570b5082d0278fa0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="d9903-103">Öğretici: Azure Active Directory Tümleştirme Convercent ile</span><span class="sxs-lookup"><span data-stu-id="d9903-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="d9903-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Convercent tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d9903-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9903-105">Convercent Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d9903-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d9903-106">Convercent erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d9903-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="d9903-107">Otomatik olarak için Convercent (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d9903-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9903-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d9903-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d9903-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9903-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9903-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d9903-110">Prerequisites</span></span>

<span data-ttu-id="d9903-111">Azure AD tümleştirme Convercent ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9903-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="d9903-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d9903-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9903-113">Bir Convercent çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="d9903-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9903-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d9903-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9903-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9903-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9903-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d9903-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9903-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9903-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9903-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d9903-118">Scenario description</span></span>
<span data-ttu-id="d9903-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d9903-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9903-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d9903-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9903-121">Galeriden Convercent ekleme</span><span class="sxs-lookup"><span data-stu-id="d9903-121">Adding Convercent from the gallery</span></span>
2. <span data-ttu-id="d9903-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d9903-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-the-gallery"></a><span data-ttu-id="d9903-123">Galeriden Convercent ekleme</span><span class="sxs-lookup"><span data-stu-id="d9903-123">Adding Convercent from the gallery</span></span>
<span data-ttu-id="d9903-124">Azure AD Convercent tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Convercent eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9903-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d9903-125">**Galeriden Convercent eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d9903-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d9903-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d9903-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9903-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d9903-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d9903-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d9903-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d9903-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d9903-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d9903-133">Arama kutusuna **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="d9903-133">In the search box, type **Convercent**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="d9903-135">Sonuçlar panelinde seçin **Convercent**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d9903-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9903-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d9903-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9903-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Convercent ile test etme</span><span class="sxs-lookup"><span data-stu-id="d9903-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9903-139">Tekli çalışmaya oturum için Azure AD Convercent karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="d9903-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="d9903-140">Diğer bir deyişle, bir Azure AD kullanıcısının Convercent ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9903-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="d9903-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Convercent içinde.</span><span class="sxs-lookup"><span data-stu-id="d9903-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="d9903-142">Yapılandırma ve Azure AD çoklu oturum açma Convercent ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9903-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d9903-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d9903-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d9903-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="d9903-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9903-145">**[Convercent test kullanıcısı oluşturma](#creating-a-convercent-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Convercent sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="d9903-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9903-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d9903-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9903-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d9903-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9903-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d9903-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9903-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Convercent uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d9903-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="d9903-150">**Azure AD çoklu oturum açma ile Convercent yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d9903-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="d9903-151">Azure portalında üzerinde **Convercent** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d9903-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d9903-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d9903-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="d9903-155">Üzerinde **Convercent etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP başlatılan modu**, aşağıdaki adımı gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d9903-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="d9903-157">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="d9903-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="d9903-158">Uygulamada yapılandırmak istiyorsanız **SP tarafından başlatılan modu**, **Convercent etki alanı ve URL'leri** bölümü aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d9903-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="d9903-160">a.</span><span class="sxs-lookup"><span data-stu-id="d9903-160">a.</span></span> <span data-ttu-id="d9903-161">Tıklatın **"Göster Gelişmiş URL ayarlarını."**</span><span class="sxs-lookup"><span data-stu-id="d9903-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="d9903-162">b.</span><span class="sxs-lookup"><span data-stu-id="d9903-162">b.</span></span> <span data-ttu-id="d9903-163">İçinde **oturum üzerinde URL'si** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="d9903-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="d9903-164">c.</span><span class="sxs-lookup"><span data-stu-id="d9903-164">c.</span></span> <span data-ttu-id="d9903-165">İçinde **geçiş durumunu** metin kutusuna, şu biçimi kullanarak değeri yazın:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="d9903-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9903-166">Bu değerleri gerçek değerleri değildir.</span><span class="sxs-lookup"><span data-stu-id="d9903-166">These values are not the real values.</span></span> <span data-ttu-id="d9903-167">Bu değerleri gerçek tanımlayıcısı, oturum üzerinde URL'si ve geçiş durumunu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9903-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="d9903-168">Kişi [Convercent istemci destek ekibi](http://support.convercent.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="d9903-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span></span>

5. <span data-ttu-id="d9903-169">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d9903-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="d9903-171">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d9903-171">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d9903-173">Uygulamanız için yapılandırılmış SSO almak için başvurun [Convercent destek ekibi](mailto:support@convercent.com) ve indirilen ile verin **meta veri XML**.</span><span class="sxs-lookup"><span data-stu-id="d9903-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="d9903-174">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d9903-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d9903-175">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="d9903-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d9903-176">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9903-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9903-177">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9903-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9903-178">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d9903-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d9903-180">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d9903-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d9903-181">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d9903-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9903-183">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d9903-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9903-185">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="d9903-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9903-187">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d9903-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9903-189">a.</span><span class="sxs-lookup"><span data-stu-id="d9903-189">a.</span></span> <span data-ttu-id="d9903-190">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9903-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9903-191">b.</span><span class="sxs-lookup"><span data-stu-id="d9903-191">b.</span></span> <span data-ttu-id="d9903-192">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d9903-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9903-193">c.</span><span class="sxs-lookup"><span data-stu-id="d9903-193">c.</span></span> <span data-ttu-id="d9903-194">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d9903-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d9903-195">d.</span><span class="sxs-lookup"><span data-stu-id="d9903-195">d.</span></span> <span data-ttu-id="d9903-196">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9903-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="d9903-197">Convercent test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9903-197">Creating a Convercent test user</span></span>

<span data-ttu-id="d9903-198">Çalışmak [Convercent destek ekibi](mailto:support@convercent.com) Convercent platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="d9903-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d9903-199">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d9903-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d9903-200">Bu bölümde, Britta Convercent için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9903-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d9903-202">**Convercent için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d9903-202">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="d9903-203">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d9903-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d9903-205">Uygulamalar listesinde **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="d9903-205">In the applications list, select **Convercent**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="d9903-207">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d9903-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d9903-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d9903-209">Click **Add** button.</span></span> <span data-ttu-id="d9903-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d9903-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d9903-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d9903-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d9903-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d9903-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9903-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d9903-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9903-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d9903-215">Testing single sign-on</span></span>

<span data-ttu-id="d9903-216">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d9903-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d9903-217">Erişim paneli Convercent parçasında tıklattığınızda, otomatik olarak Convercent uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="d9903-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>
<span data-ttu-id="d9903-218">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9903-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d9903-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d9903-219">Additional resources</span></span>

* [<span data-ttu-id="d9903-220">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="d9903-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9903-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d9903-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

