---
title: "Öğretici: Azure Active Directory Tümleştirme Sigortası ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Sigortası arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9a91e22faced9e126043bebefd85c307dbdf933d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="35da3-103">Öğretici: Azure Active Directory Tümleştirme Sigortası ile</span><span class="sxs-lookup"><span data-stu-id="35da3-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="35da3-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Sigortası tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="35da3-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35da3-105">Sigortası Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="35da3-105">Integrating Fuse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="35da3-106">Sigortası erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35da3-106">You can control in Azure AD who has access to Fuse.</span></span>
- <span data-ttu-id="35da3-107">Otomatik olarak için Sigortası (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35da3-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="35da3-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="35da3-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="35da3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35da3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35da3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="35da3-110">Prerequisites</span></span>

<span data-ttu-id="35da3-111">Azure AD tümleştirme Sigortası ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="35da3-111">To configure Azure AD integration with Fuse, you need the following items:</span></span>

- <span data-ttu-id="35da3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="35da3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35da3-113">Bir Sigortası çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="35da3-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35da3-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="35da3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35da3-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="35da3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35da3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="35da3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35da3-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35da3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35da3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="35da3-118">Scenario description</span></span>
<span data-ttu-id="35da3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="35da3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35da3-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="35da3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35da3-121">Galeriden Sigortası ekleme</span><span class="sxs-lookup"><span data-stu-id="35da3-121">Add Fuse from the gallery</span></span>
2. <span data-ttu-id="35da3-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="35da3-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-the-gallery"></a><span data-ttu-id="35da3-123">Galeriden Sigortası ekleme</span><span class="sxs-lookup"><span data-stu-id="35da3-123">Add Fuse from the gallery</span></span>
<span data-ttu-id="35da3-124">Azure AD Sigortası tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Sigortası eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="35da3-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="35da3-125">**Galeriden Sigortası eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35da3-125">**To add Fuse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="35da3-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="35da3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="35da3-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="35da3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="35da3-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="35da3-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="35da3-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="35da3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="35da3-133">Arama kutusuna **Sigortası**seçin **Sigortası** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="35da3-133">In the search box, type **Fuse**, select **Fuse** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde Sigortası](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="35da3-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="35da3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="35da3-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Sigortası sınayın.</span><span class="sxs-lookup"><span data-stu-id="35da3-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35da3-137">Tekli çalışmaya oturum için Azure AD Sigortası karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="35da3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span></span> <span data-ttu-id="35da3-138">Diğer bir deyişle, bir Azure AD kullanıcısının Sigortası ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="35da3-138">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span></span>

<span data-ttu-id="35da3-139">Değeri Sigortası içinde atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="35da3-139">In Fuse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="35da3-140">Yapılandırma ve Azure AD çoklu oturum açma Sigortası ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="35da3-140">To configure and test Azure AD single sign-on with Fuse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="35da3-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="35da3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="35da3-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="35da3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35da3-143">**[Sigortası test kullanıcısı oluşturma](#create-a-fuse-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Sigortası sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="35da3-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="35da3-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="35da3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35da3-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="35da3-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="35da3-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="35da3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="35da3-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Sigortası uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="35da3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="35da3-148">**Azure AD çoklu oturum açma ile Sigortası yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35da3-148">**To configure Azure AD single sign-on with Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="35da3-149">Azure portalında üzerinde **Sigortası** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="35da3-149">In the Azure portal, on the **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="35da3-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="35da3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="35da3-153">Üzerinde **Sigortası etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35da3-153">On the **Fuse Domain and URLs** section, perform the following steps:</span></span>

    ![Etki alanı ve URL'leri tek oturum açma bilgilerini Sigortası](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="35da3-155">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="35da3-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35da3-156">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="35da3-156">This value is not real.</span></span> <span data-ttu-id="35da3-157">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="35da3-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="35da3-158">Kişi [Sigortası istemci destek ekibi](mailto:support@fusion-universal.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="35da3-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) to get this value.</span></span> 
 
4. <span data-ttu-id="35da3-159">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="35da3-159">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="35da3-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="35da3-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="35da3-163">Üzerinde **Sigortası yapılandırma** 'yi tıklatın **yapılandırma Sigortası** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="35da3-163">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span></span> <span data-ttu-id="35da3-164">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="35da3-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sigortası yapılandırma](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="35da3-166">Uygulamanız için yapılandırılmış SSO almak için başvurun [Sigortası destek ekibi](mailto:support@fusion-universal.com) ve ile aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="35da3-166">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span></span>

    * <span data-ttu-id="35da3-167">İndirilen **(ham) sertifika dosyası**</span><span class="sxs-lookup"><span data-stu-id="35da3-167">The downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="35da3-168">**SAML çoklu oturum açma hizmeti URL'si**</span><span class="sxs-lookup"><span data-stu-id="35da3-168">The **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="35da3-169">**SAML varlık kimliği**</span><span class="sxs-lookup"><span data-stu-id="35da3-169">The **SAML Entity ID**</span></span>
    * <span data-ttu-id="35da3-170">**Oturum kapatma URL'si**</span><span class="sxs-lookup"><span data-stu-id="35da3-170">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="35da3-171">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="35da3-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="35da3-172">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="35da3-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="35da3-173">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35da3-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="35da3-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="35da3-174">Create an Azure AD test user</span></span>

<span data-ttu-id="35da3-175">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="35da3-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="35da3-177">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35da3-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="35da3-178">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="35da3-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="35da3-180">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="35da3-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="35da3-182">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="35da3-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="35da3-184">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35da3-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="35da3-186">a.</span><span class="sxs-lookup"><span data-stu-id="35da3-186">a.</span></span> <span data-ttu-id="35da3-187">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35da3-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35da3-188">b.</span><span class="sxs-lookup"><span data-stu-id="35da3-188">b.</span></span> <span data-ttu-id="35da3-189">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="35da3-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="35da3-190">c.</span><span class="sxs-lookup"><span data-stu-id="35da3-190">c.</span></span> <span data-ttu-id="35da3-191">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="35da3-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="35da3-192">d.</span><span class="sxs-lookup"><span data-stu-id="35da3-192">d.</span></span> <span data-ttu-id="35da3-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35da3-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="35da3-194">Sigortası test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="35da3-194">Create a Fuse test user</span></span>

<span data-ttu-id="35da3-195">Bu bölümde, içinde Sigortası Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35da3-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="35da3-196">Lütfen çalışmak [Sigortası destek ekibi](mailto:support@fusion-universal.com) Sigortası platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="35da3-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="35da3-197">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="35da3-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="35da3-198">Bu bölümde, Britta sigortası için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="35da3-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fuse.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="35da3-200">**Britta Simon sigortası için atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="35da3-200">**To assign Britta Simon to Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="35da3-201">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="35da3-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="35da3-203">Uygulamalar listesinde **Sigortası**.</span><span class="sxs-lookup"><span data-stu-id="35da3-203">In the applications list, select **Fuse**.</span></span>

    ![Uygulamalar listesinde Sigortası bağlantı](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="35da3-205">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="35da3-205">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="35da3-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="35da3-207">Click **Add** button.</span></span> <span data-ttu-id="35da3-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="35da3-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="35da3-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="35da3-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="35da3-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="35da3-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35da3-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="35da3-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="35da3-213">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="35da3-213">Test single sign-on</span></span>

<span data-ttu-id="35da3-214">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="35da3-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="35da3-215">Erişim paneli Sigortası parçasında tıklattığınızda, otomatik olarak Sigortası uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="35da3-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span></span>
<span data-ttu-id="35da3-216">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="35da3-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="35da3-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="35da3-217">Additional resources</span></span>

* [<span data-ttu-id="35da3-218">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="35da3-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35da3-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="35da3-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

