---
title: "Öğretici: Azure Active Directory Tümleştirme ile Evidence.com | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Evidence.com arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a9c474cfc648fc8a306d736c89a4813d82c133ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="eccc0-103">Öğretici: Azure Active Directory Tümleştirme Evidence.com ile</span><span class="sxs-lookup"><span data-stu-id="eccc0-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="eccc0-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Evidence.com tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="eccc0-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eccc0-105">Evidence.com Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="eccc0-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eccc0-106">Evidence.com erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eccc0-106">You can control in Azure AD who has access to Evidence.com.</span></span>
- <span data-ttu-id="eccc0-107">Otomatik olarak için Evidence.com (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eccc0-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="eccc0-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="eccc0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="eccc0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eccc0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eccc0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eccc0-110">Prerequisites</span></span>

<span data-ttu-id="eccc0-111">Azure AD tümleştirme Evidence.com ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="eccc0-111">To configure Azure AD integration with Evidence.com, you need the following items:</span></span>

- <span data-ttu-id="eccc0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="eccc0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eccc0-113">Bir Evidence.com çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="eccc0-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eccc0-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="eccc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eccc0-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="eccc0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eccc0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="eccc0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eccc0-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eccc0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eccc0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="eccc0-118">Scenario description</span></span>
<span data-ttu-id="eccc0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="eccc0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eccc0-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="eccc0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eccc0-121">Galeriden Evidence.com ekleme</span><span class="sxs-lookup"><span data-stu-id="eccc0-121">Adding Evidence.com from the gallery</span></span>
2. <span data-ttu-id="eccc0-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="eccc0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-the-gallery"></a><span data-ttu-id="eccc0-123">Galeriden Evidence.com ekleme</span><span class="sxs-lookup"><span data-stu-id="eccc0-123">Adding Evidence.com from the gallery</span></span>
<span data-ttu-id="eccc0-124">Azure AD Evidence.com tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Evidence.com eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eccc0-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eccc0-125">**Galeriden Evidence.com eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eccc0-125">**To add Evidence.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eccc0-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="eccc0-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="eccc0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eccc0-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eccc0-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="eccc0-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="eccc0-133">Arama kutusuna **Evidence.com**seçin **Evidence.com** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="eccc0-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="eccc0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="eccc0-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Evidence.com sınayın.</span><span class="sxs-lookup"><span data-stu-id="eccc0-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eccc0-137">Tekli çalışmaya oturum için Azure AD Evidence.com karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="eccc0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span></span> <span data-ttu-id="eccc0-138">Diğer bir deyişle, bir Azure AD kullanıcısının Evidence.com ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eccc0-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span></span>

<span data-ttu-id="eccc0-139">Evidence.com içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="eccc0-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eccc0-140">Yapılandırma ve Azure AD çoklu oturum açma Evidence.com ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="eccc0-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eccc0-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="eccc0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eccc0-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="eccc0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eccc0-143">**[Evidence.com test kullanıcısı oluşturma](#create-a-evidencecom-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Evidence.com sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="eccc0-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eccc0-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="eccc0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eccc0-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="eccc0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="eccc0-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="eccc0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="eccc0-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Evidence.com uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="eccc0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="eccc0-148">**Azure AD çoklu oturum açma ile Evidence.com yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eccc0-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="eccc0-149">Azure portalında üzerinde **Evidence.com** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="eccc0-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="eccc0-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="eccc0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="eccc0-153">Üzerinde **Evidence.com etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eccc0-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span></span>

    ![Evidence.com etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="eccc0-155">a.</span><span class="sxs-lookup"><span data-stu-id="eccc0-155">a.</span></span> <span data-ttu-id="eccc0-156">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="eccc0-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="eccc0-157">b.</span><span class="sxs-lookup"><span data-stu-id="eccc0-157">b.</span></span> <span data-ttu-id="eccc0-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="eccc0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eccc0-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="eccc0-159">These values are not real.</span></span> <span data-ttu-id="eccc0-160">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="eccc0-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eccc0-161">Kişi [Evidence.com istemci destek ekibi](https://communities.taser.com/support/SupportContactUs?typ=LE) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="eccc0-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span></span> 

4. <span data-ttu-id="eccc0-162">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eccc0-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="eccc0-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eccc0-166">Üzerinde **Evidence.com yapılandırma** 'yi tıklatın **yapılandırma Evidence.com** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="eccc0-167">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="eccc0-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Evidence.com yapılandırma](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="eccc0-169">Bir oturum açma, Evidence.com için ayrı bir web tarayıcı penceresinde Kiracı yönetici olarak ve gidin **yönetici** sekmesi</span><span class="sxs-lookup"><span data-stu-id="eccc0-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>

8. <span data-ttu-id="eccc0-170">Tıklayın **Teşkilatı çoklu oturum açma**</span><span class="sxs-lookup"><span data-stu-id="eccc0-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="eccc0-171">Seçin **SAML temel çoklu oturum açma**</span><span class="sxs-lookup"><span data-stu-id="eccc0-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="eccc0-172">Kopya **SAML varlık kimliği**, **SAML çoklu oturum açma hizmet URL'si** ve **Sign-Out URL** Azure portalında ve Evidence.com karşılık gelen alanlara gösterilen değerleri.</span><span class="sxs-lookup"><span data-stu-id="eccc0-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="eccc0-173">İndirilen Certificate(Base64) dosyasını Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **güvenlik sertifikası** kutusu.</span><span class="sxs-lookup"><span data-stu-id="eccc0-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span></span> 

12. <span data-ttu-id="eccc0-174">Yapılandırmayı Evidence.com kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eccc0-174">Save the configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="eccc0-175">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="eccc0-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eccc0-176">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="eccc0-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eccc0-177">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eccc0-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="eccc0-178">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eccc0-178">Create an Azure AD test user</span></span>

<span data-ttu-id="eccc0-179">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="eccc0-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="eccc0-181">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eccc0-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eccc0-182">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="eccc0-184">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="eccc0-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="eccc0-186">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="eccc0-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="eccc0-188">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="eccc0-188">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="eccc0-190">a.</span><span class="sxs-lookup"><span data-stu-id="eccc0-190">a.</span></span> <span data-ttu-id="eccc0-191">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eccc0-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eccc0-192">b.</span><span class="sxs-lookup"><span data-stu-id="eccc0-192">b.</span></span> <span data-ttu-id="eccc0-193">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="eccc0-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="eccc0-194">c.</span><span class="sxs-lookup"><span data-stu-id="eccc0-194">c.</span></span> <span data-ttu-id="eccc0-195">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="eccc0-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="eccc0-196">d.</span><span class="sxs-lookup"><span data-stu-id="eccc0-196">d.</span></span> <span data-ttu-id="eccc0-197">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eccc0-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="eccc0-198">Evidence.com test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eccc0-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="eccc0-199">Azure AD kullanıcıların oturum açabilmesi için Evidence.com uygulama erişimi için hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eccc0-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="eccc0-200">Bu bölümde Evidence.com içinde Azure AD kullanıcı hesaplarının nasıl oluşturulacağı açıklanmaktadır</span><span class="sxs-lookup"><span data-stu-id="eccc0-200">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="eccc0-201">**Bir kullanıcı hesabında Evidence.com sağlamak için:**</span><span class="sxs-lookup"><span data-stu-id="eccc0-201">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="eccc0-202">Bir web tarayıcısı penceresinde Evidence.com şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eccc0-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="eccc0-203">Gidin **yönetici** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-203">Navigate to **Admin** tab.</span></span>

3. <span data-ttu-id="eccc0-204">Tıklayın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="eccc0-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="eccc0-205">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-205">Click the **Add** button.</span></span>

5. <span data-ttu-id="eccc0-206">**E-posta adresi** eklenen kullanıcı erişimi vermek istediğiniz Azure AD içinde kullanıcıların kullanıcı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="eccc0-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="eccc0-207">Kullanıcı adı ve e-posta adresi kuruluşunuzun aynı değeri emin değilseniz, kullanabileceğiniz **Evidence.com > öznitelikler > çoklu oturum açma** bölüm olmasını Evidence.com için gönderilen nameidenitifer değiştirmek için Azure portalı e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="eccc0-208">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="eccc0-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="eccc0-209">Bu bölümde, Britta Evidence.com için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="eccc0-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="eccc0-211">**Evidence.com için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="eccc0-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="eccc0-212">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="eccc0-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="eccc0-214">Uygulamalar listesinde **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="eccc0-214">In the applications list, select **Evidence.com**.</span></span>

    ![Uygulamalar listesinde Evidence.com bağlantı](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="eccc0-216">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="eccc0-216">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="eccc0-218">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eccc0-218">Click **Add** button.</span></span> <span data-ttu-id="eccc0-219">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eccc0-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="eccc0-221">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="eccc0-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eccc0-222">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eccc0-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eccc0-223">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="eccc0-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="eccc0-224">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="eccc0-224">Test single sign-on</span></span>

<span data-ttu-id="eccc0-225">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="eccc0-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="eccc0-226">Erişim paneli Evidence.com parçasında tıklattığınızda, otomatik olarak Evidence.com uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="eccc0-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span></span>
<span data-ttu-id="eccc0-227">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eccc0-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eccc0-228">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="eccc0-228">Additional resources</span></span>

* [<span data-ttu-id="eccc0-229">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="eccc0-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eccc0-230">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="eccc0-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

