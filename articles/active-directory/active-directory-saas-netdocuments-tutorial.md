---
title: "Öğretici: Azure Active Directory Tümleştirme ile NetDocuments | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile NetDocuments arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 87c3338d611daa837aa5f079c4b68e0e6fc58455
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="201e1-103">Öğretici: Azure Active Directory Tümleştirme NetDocuments ile</span><span class="sxs-lookup"><span data-stu-id="201e1-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="201e1-104">Bu öğreticide, Azure Active Directory (Azure AD) ile NetDocuments tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="201e1-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="201e1-105">NetDocuments Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="201e1-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="201e1-106">NetDocuments erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="201e1-106">You can control in Azure AD who has access to NetDocuments</span></span>
- <span data-ttu-id="201e1-107">Otomatik olarak için NetDocuments (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="201e1-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="201e1-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="201e1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="201e1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="201e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="201e1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="201e1-110">Prerequisites</span></span>

<span data-ttu-id="201e1-111">Azure AD tümleştirme NetDocuments ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="201e1-111">To configure Azure AD integration with NetDocuments, you need the following items:</span></span>

- <span data-ttu-id="201e1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="201e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="201e1-113">Bir NetDocuments çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="201e1-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="201e1-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="201e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="201e1-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="201e1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="201e1-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="201e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="201e1-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="201e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="201e1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="201e1-118">Scenario description</span></span>
<span data-ttu-id="201e1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="201e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="201e1-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="201e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="201e1-121">Galeriden NetDocuments ekleme</span><span class="sxs-lookup"><span data-stu-id="201e1-121">Adding NetDocuments from the gallery</span></span>
2. <span data-ttu-id="201e1-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="201e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-the-gallery"></a><span data-ttu-id="201e1-123">Galeriden NetDocuments ekleme</span><span class="sxs-lookup"><span data-stu-id="201e1-123">Adding NetDocuments from the gallery</span></span>
<span data-ttu-id="201e1-124">Azure AD NetDocuments tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden NetDocuments eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="201e1-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="201e1-125">**Galeriden NetDocuments eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="201e1-125">**To add NetDocuments from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="201e1-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="201e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="201e1-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="201e1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="201e1-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="201e1-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="201e1-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="201e1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="201e1-133">Arama kutusuna **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="201e1-133">In the search box, type **NetDocuments**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="201e1-135">Sonuçlar panelinde seçin **NetDocuments**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="201e1-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="201e1-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="201e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="201e1-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı NetDocuments sınayın.</span><span class="sxs-lookup"><span data-stu-id="201e1-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="201e1-139">Tekli çalışmaya oturum için Azure AD NetDocuments karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="201e1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span></span> <span data-ttu-id="201e1-140">Diğer bir deyişle, bir Azure AD kullanıcısının NetDocuments ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="201e1-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span></span>

<span data-ttu-id="201e1-141">NetDocuments içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="201e1-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="201e1-142">Yapılandırma ve Azure AD çoklu oturum açma NetDocuments ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="201e1-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="201e1-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="201e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="201e1-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="201e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="201e1-145">**[NetDocuments test kullanıcısı oluşturma](#creating-a-netdocuments-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı NetDocuments sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="201e1-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="201e1-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="201e1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="201e1-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="201e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="201e1-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="201e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="201e1-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma NetDocuments uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="201e1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="201e1-150">**Azure AD çoklu oturum açma ile NetDocuments yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="201e1-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="201e1-151">Azure portalında üzerinde **NetDocuments** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="201e1-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="201e1-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="201e1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="201e1-155">Üzerinde **NetDocuments etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="201e1-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="201e1-157">a.</span><span class="sxs-lookup"><span data-stu-id="201e1-157">a.</span></span> <span data-ttu-id="201e1-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="201e1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="201e1-159">b.</span><span class="sxs-lookup"><span data-stu-id="201e1-159">b.</span></span> <span data-ttu-id="201e1-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="201e1-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="201e1-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="201e1-161">These values are not real.</span></span> <span data-ttu-id="201e1-162">Bu değerler gerçek oturum açma URL'si ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="201e1-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="201e1-163">Kişi [NetDocuments destek ekibi](https://support.netdocuments.com/hc/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="201e1-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span></span>
 
4. <span data-ttu-id="201e1-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="201e1-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="201e1-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="201e1-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="201e1-168">Farklı web tarayıcısı penceresinde NetDocuments şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="201e1-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="201e1-169">Git **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="201e1-169">Go to **Admin**.</span></span>

8. <span data-ttu-id="201e1-170">Tıklatın **ekleme ve kaldırma kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="201e1-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="201e1-171">![Depo](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "deposu")</span><span class="sxs-lookup"><span data-stu-id="201e1-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="201e1-172">Tıklatın **Gelişmiş kimlik doğrulama Seçenekleri Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="201e1-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="201e1-173">![Gelişmiş kimlik doğrulama Seçenekleri Yapılandır](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Gelişmiş kimlik doğrulama seçeneklerini yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="201e1-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="201e1-174">Üzerinde **Federal Kimlik** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="201e1-174">On the **Federated Identity** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="201e1-175">![Identitty Federasyon](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identitty Federasyon")</span><span class="sxs-lookup"><span data-stu-id="201e1-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="201e1-176">a.</span><span class="sxs-lookup"><span data-stu-id="201e1-176">a.</span></span> <span data-ttu-id="201e1-177">Olarak **kimlik sunucu türü Federasyon**seçin **Active Directory Federasyon Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="201e1-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="201e1-178">b.</span><span class="sxs-lookup"><span data-stu-id="201e1-178">b.</span></span> <span data-ttu-id="201e1-179">Tıklatın **dosya**, Azure Portalı'ndan indirilen indirilen meta veri dosyasını karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="201e1-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="201e1-180">c.</span><span class="sxs-lookup"><span data-stu-id="201e1-180">c.</span></span> <span data-ttu-id="201e1-181">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="201e1-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="201e1-182">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="201e1-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="201e1-183">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="201e1-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="201e1-184">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="201e1-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="201e1-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="201e1-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="201e1-186">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="201e1-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="201e1-188">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="201e1-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="201e1-189">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="201e1-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="201e1-191">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="201e1-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="201e1-193">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="201e1-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="201e1-195">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="201e1-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="201e1-197">a.</span><span class="sxs-lookup"><span data-stu-id="201e1-197">a.</span></span> <span data-ttu-id="201e1-198">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="201e1-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="201e1-199">b.</span><span class="sxs-lookup"><span data-stu-id="201e1-199">b.</span></span> <span data-ttu-id="201e1-200">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="201e1-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="201e1-201">c.</span><span class="sxs-lookup"><span data-stu-id="201e1-201">c.</span></span> <span data-ttu-id="201e1-202">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="201e1-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="201e1-203">d.</span><span class="sxs-lookup"><span data-stu-id="201e1-203">d.</span></span> <span data-ttu-id="201e1-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="201e1-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="201e1-205">NetDocuments test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="201e1-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="201e1-206">Azure AD kullanıcıları için NetDocuments oturum açmak etkinleştirmek için bunların NetDocuments sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="201e1-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="201e1-207">NetDocuments söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="201e1-207">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="201e1-208">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="201e1-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="201e1-209">Oturum SING, **NetDocuments** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="201e1-209">Sing on to your **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="201e1-210">Üstteki menüde tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="201e1-210">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="201e1-211">![Yönetici](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="201e1-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="201e1-212">Tıklatın **ekleme ve kaldırma kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="201e1-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="201e1-213">![Depo](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "deposu")</span><span class="sxs-lookup"><span data-stu-id="201e1-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="201e1-214">İçinde **e-posta adresi** metin kutusu, geçerli bir Azure Active Directory hesabı sağlamak istediğiniz ve ardından e-posta adresini yazın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="201e1-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="201e1-215">![E-posta adresi](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "e-posta adresi")</span><span class="sxs-lookup"><span data-stu-id="201e1-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="201e1-216">Azure Active Directory hesap sahibi etkin duruma gelmesi hesabı onaylamak için bir bağlantı içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="201e1-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="201e1-217">API tarafından NetDocuments sağlamak için Azure Active Directory kullanıcı hesapları sağlanan veya herhangi diğer NetDocuments kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="201e1-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="201e1-218">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="201e1-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="201e1-219">Bu bölümde, Britta NetDocuments için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="201e1-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="201e1-221">**NetDocuments için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="201e1-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="201e1-222">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="201e1-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="201e1-224">Uygulamalar listesinde **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="201e1-224">In the applications list, select **NetDocuments**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="201e1-226">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="201e1-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="201e1-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="201e1-228">Click **Add** button.</span></span> <span data-ttu-id="201e1-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="201e1-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="201e1-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="201e1-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="201e1-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="201e1-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="201e1-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="201e1-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="201e1-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="201e1-234">Testing single sign-on</span></span>

<span data-ttu-id="201e1-235">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="201e1-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="201e1-236">Erişim paneli NetDocuments parçasında tıklattığınızda, otomatik olarak NetDocuments uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="201e1-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span></span>
<span data-ttu-id="201e1-237">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="201e1-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="201e1-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="201e1-238">Additional resources</span></span>

* [<span data-ttu-id="201e1-239">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="201e1-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="201e1-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="201e1-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

