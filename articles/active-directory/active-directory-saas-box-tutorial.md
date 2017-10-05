---
title: "Öğretici: Azure Active Directory Tümleştirme kutusuyla | Microsoft Docs"
description: "Çoklu oturum açma kutusunu ve Azure Active Directory arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 2cc2afe8ff3f0063224c94eb0b8135347051b0aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="60533-103">Öğretici: Azure Active Directory Tümleştirme kutusu</span><span class="sxs-lookup"><span data-stu-id="60533-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="60533-104">Bu öğreticide, Azure Active Directory (Azure AD) ile kutusunu tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="60533-104">In this tutorial, you learn how to integrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60533-105">Kutusunu Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="60533-105">Integrating Box with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60533-106">Kutusuna erişimi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="60533-106">You can control in Azure AD who has access to Box</span></span>
- <span data-ttu-id="60533-107">Otomatik olarak kutusuna (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="60533-107">You can enable your users to automatically get signed-on to Box (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60533-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="60533-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="60533-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60533-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60533-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="60533-110">Prerequisites</span></span>

<span data-ttu-id="60533-111">Azure AD tümleştirme kutusuyla yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="60533-111">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="60533-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="60533-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60533-113">Bir kutusunu çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="60533-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60533-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="60533-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60533-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="60533-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60533-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="60533-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60533-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60533-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60533-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="60533-118">Scenario description</span></span>
<span data-ttu-id="60533-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="60533-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60533-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="60533-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60533-121">Galeriden kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="60533-121">Adding Box from the gallery</span></span>
2. <span data-ttu-id="60533-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="60533-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-the-gallery"></a><span data-ttu-id="60533-123">Galeriden kutusu ekleme</span><span class="sxs-lookup"><span data-stu-id="60533-123">Adding Box from the gallery</span></span>
<span data-ttu-id="60533-124">Azure AD kutusuna tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden kutusu eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="60533-124">To configure the integration of Box into Azure AD, you need to add Box from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60533-125">**Galeriden kutusu eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="60533-125">**To add Box from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60533-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="60533-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60533-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="60533-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60533-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="60533-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="60533-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="60533-131">Click **New application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="60533-133">Arama kutusuna **kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="60533-133">In the search box, type **Box**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="60533-135">Sonuçlar panelinde seçin **kutusunu**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="60533-135">In the results panel, select **Box**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60533-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="60533-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60533-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı kutusuyla test etme</span><span class="sxs-lookup"><span data-stu-id="60533-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="60533-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen kutusunda bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="60533-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Box is to a user in Azure AD.</span></span> <span data-ttu-id="60533-140">Diğer bir deyişle, bir Azure AD kullanıcısının kutusunda ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="60533-140">In other words, a link relationship between an Azure AD user and the related user in Box needs to be established.</span></span>

<span data-ttu-id="60533-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** kutusunda.</span><span class="sxs-lookup"><span data-stu-id="60533-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Box.</span></span>

<span data-ttu-id="60533-142">Yapılandırmak ve Azure AD çoklu oturum açma kutusuyla sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="60533-142">To configure and test Azure AD single sign-on with Box, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60533-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="60533-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60533-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="60533-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60533-145">**[Kutusunu test kullanıcısı oluşturma](#creating-a-box-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı kutusunu sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="60533-145">**[Creating a Box test user](#creating-a-box-test-user)** - to have a counterpart of Britta Simon in Box that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="60533-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="60533-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60533-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="60533-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60533-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="60533-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60533-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma kutusunu uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="60533-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="60533-150">**Azure AD çoklu oturum açma kutusuyla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="60533-150">**To configure Azure AD single sign-on with Box, perform the following steps:**</span></span>

1. <span data-ttu-id="60533-151">Azure portalında üzerinde **kutusunu** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="60533-151">In the Azure portal, on the **Box** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="60533-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="60533-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="60533-155">Üzerinde **kutusunu etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="60533-155">On the **Box Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="60533-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="60533-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="60533-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="60533-158">This value is not real.</span></span> <span data-ttu-id="60533-159">Değerin gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="60533-159">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="60533-160">Kişi [kutusunu istemci destek ekibi](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="60533-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) to get this value.</span></span> 
 
4. <span data-ttu-id="60533-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="60533-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="60533-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="60533-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="60533-165">Uygulamanız için yapılandırılmış SSO almak için başvurun [kutusunu istemci destek ekibi](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) ve indirilen XML dosyasıyla verin.</span><span class="sxs-lookup"><span data-stu-id="60533-165">To get SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with the downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="60533-166">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="60533-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60533-167">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="60533-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60533-168">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="60533-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60533-169">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="60533-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="60533-170">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="60533-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="60533-172">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="60533-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60533-173">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="60533-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60533-175">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="60533-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60533-177">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="60533-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60533-179">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="60533-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60533-181">a.</span><span class="sxs-lookup"><span data-stu-id="60533-181">a.</span></span> <span data-ttu-id="60533-182">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60533-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60533-183">b.</span><span class="sxs-lookup"><span data-stu-id="60533-183">b.</span></span> <span data-ttu-id="60533-184">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="60533-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60533-185">c.</span><span class="sxs-lookup"><span data-stu-id="60533-185">c.</span></span> <span data-ttu-id="60533-186">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="60533-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60533-187">d.</span><span class="sxs-lookup"><span data-stu-id="60533-187">d.</span></span> <span data-ttu-id="60533-188">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="60533-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="60533-189">Kutusunu test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="60533-189">Creating a Box test user</span></span>

<span data-ttu-id="60533-190">Bu bölümde, Britta Simon adlı bir kullanıcı kutusunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="60533-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="60533-191">Kutusu yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="60533-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="60533-192">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="60533-192">There is no action item for you in this section.</span></span> <span data-ttu-id="60533-193">Bir kullanıcı zaten kutusunda yoksa, kutusunu erişmeyi denediğinde yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="60533-193">If a user doesn't already exist in Box, a new one is created when you attempt to access Box.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60533-194">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="60533-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="60533-195">Bu bölümde, Britta kutusuna erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="60533-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Box.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="60533-197">**Britta Simon kutusuna atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="60533-197">**To assign Britta Simon to Box, perform the following steps:**</span></span>

1. <span data-ttu-id="60533-198">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="60533-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="60533-200">Uygulamalar listesinde **kutusunu**.</span><span class="sxs-lookup"><span data-stu-id="60533-200">In the applications list, select **Box**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="60533-202">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="60533-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="60533-204">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="60533-204">Click **Add** button.</span></span> <span data-ttu-id="60533-205">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="60533-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="60533-207">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="60533-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="60533-208">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="60533-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60533-209">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="60533-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60533-210">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="60533-210">Testing single sign-on</span></span>

<span data-ttu-id="60533-211">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="60533-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60533-212">Erişim paneli kutusunu parçasında tıklattığınızda açan kutusunu uygulamanıza oturum açma sayfasına almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="60533-212">When you click the Box tile in the Access Panel, you should get login page to get signed-on to your Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60533-213">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="60533-213">Additional resources</span></span>

* [<span data-ttu-id="60533-214">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="60533-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60533-215">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="60533-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="60533-216">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="60533-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

