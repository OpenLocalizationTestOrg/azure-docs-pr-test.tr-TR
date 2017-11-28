---
title: "Öğretici: Cisco Spark Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Cisco Spark arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: a0a221622afe1c801a331e2319f3a7ace3111dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="1a432-103">Öğretici: Cisco Spark Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1a432-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="1a432-104">Bu öğreticide, Cisco Spark Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1a432-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a432-105">Cisco Spark Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1a432-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1a432-106">Cisco Spark erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1a432-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="1a432-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için Cisco Spark açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1a432-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a432-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="1a432-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1a432-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a432-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a432-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1a432-110">Prerequisites</span></span>

<span data-ttu-id="1a432-111">Azure AD tümleştirme Cisco Spark ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="1a432-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="1a432-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1a432-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a432-113">Bir Cisco Spark çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="1a432-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a432-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1a432-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a432-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1a432-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a432-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1a432-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a432-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a432-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a432-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1a432-118">Scenario description</span></span>
<span data-ttu-id="1a432-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1a432-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a432-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1a432-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a432-121">Cisco Spark Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="1a432-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="1a432-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1a432-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="1a432-123">Cisco Spark Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="1a432-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="1a432-124">Azure AD Cisco Spark tümleştirilmesi yapılandırmak için Cisco Spark Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a432-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1a432-125">**Cisco Spark Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1a432-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1a432-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1a432-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a432-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1a432-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1a432-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1a432-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="1a432-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1a432-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="1a432-133">Arama kutusuna **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="1a432-133">In the search box, type **Cisco Spark**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="1a432-135">Sonuçlar panelinde seçin **Cisco Spark**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1a432-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a432-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1a432-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a432-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Cisco "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Spark ile test etme</span><span class="sxs-lookup"><span data-stu-id="1a432-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1a432-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Cisco Spark bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="1a432-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="1a432-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Cisco Spark arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a432-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="1a432-141">Cisco Spark değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1a432-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1a432-142">Yapılandırma ve Azure AD çoklu oturum açma Cisco Spark ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1a432-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1a432-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1a432-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1a432-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="1a432-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a432-145">**[Cisco Spark test kullanıcısı oluşturma](#creating-a-cisco-spark-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Cisco Spark sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="1a432-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a432-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1a432-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a432-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1a432-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a432-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1a432-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a432-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Cisco Spark uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1a432-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="1a432-150">**Azure AD çoklu oturum açma ile Cisco Spark yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1a432-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="1a432-151">Azure portalında üzerinde **Cisco Spark** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1a432-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="1a432-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1a432-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="1a432-155">Üzerinde **Cisco Spark etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1a432-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="1a432-157">a.</span><span class="sxs-lookup"><span data-stu-id="1a432-157">a.</span></span> <span data-ttu-id="1a432-158">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="1a432-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="1a432-159">b.</span><span class="sxs-lookup"><span data-stu-id="1a432-159">b.</span></span> <span data-ttu-id="1a432-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="1a432-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a432-161">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="1a432-161">This value is not real.</span></span> <span data-ttu-id="1a432-162">Bu değer gerçek tanımlayıcısı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1a432-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="1a432-163">Kişi [Cisco Spark istemci destek ekibi](https://support.ciscospark.com/) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="1a432-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
4. <span data-ttu-id="1a432-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1a432-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="1a432-166">Cisco Spark uygulama özel öznitelikler içerecek şekilde SAML onaylar bekler.</span><span class="sxs-lookup"><span data-stu-id="1a432-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="1a432-167">Bu uygulama için aşağıdaki öznitelikleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a432-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="1a432-168">Bu öznitelik değerlerini yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="1a432-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="1a432-169">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="1a432-169">The following screenshot shows an example for this.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="1a432-171">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, yukarıdaki resimde gösterildiği gibi SAML belirteci özniteliği yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1a432-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="1a432-172">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="1a432-172">Attribute Name</span></span>  | <span data-ttu-id="1a432-173">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="1a432-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="1a432-174">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="1a432-174">uid</span></span>    | <span data-ttu-id="1a432-175">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="1a432-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="1a432-176">a.</span><span class="sxs-lookup"><span data-stu-id="1a432-176">a.</span></span> <span data-ttu-id="1a432-177">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1a432-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="1a432-180">b.</span><span class="sxs-lookup"><span data-stu-id="1a432-180">b.</span></span> <span data-ttu-id="1a432-181">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="1a432-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1a432-182">c.</span><span class="sxs-lookup"><span data-stu-id="1a432-182">c.</span></span> <span data-ttu-id="1a432-183">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="1a432-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1a432-184">d.</span><span class="sxs-lookup"><span data-stu-id="1a432-184">d.</span></span> <span data-ttu-id="1a432-185">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1a432-185">Click **Ok**.</span></span>

7. <span data-ttu-id="1a432-186">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1a432-186">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1a432-188">Oturum [Cisco bulut işbirliği Yönetimi](https://admin.ciscospark.com/) tam yönetici kimlik bilgilerinizle.</span><span class="sxs-lookup"><span data-stu-id="1a432-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="1a432-189">Seçin **ayarları** ve altında **kimlik doğrulaması** 'yi tıklatın **Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="1a432-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="1a432-191">Seçin **3. taraf kimlik sağlayıcısı tümleştirin. (Gelişmiş)**  ve sonraki ekranına gidin.</span><span class="sxs-lookup"><span data-stu-id="1a432-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

11. <span data-ttu-id="1a432-192">Üzerinde **IDP meta verileri içeri aktarma** sayfasında, ya da sürükle ve Azure AD meta veri dosyası sayfaya bırak veya bulun ve Azure AD meta veri dosyası karşıya yüklemek için dosya tarayıcısı seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1a432-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="1a432-193">Ardından, seçin **meta veriler (daha güvenli) bir sertifika yetkilisi tarafından imzalanan sertifika gerekli** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1a432-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="1a432-195">Seçin **SSO Bağlantıyı Sına**ve yeni bir tarayıcı sekmesinde oturum açtığında, Azure AD ile oturum açarak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1a432-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="1a432-196">Geri dönüp **Cisco bulut işbirliği Yönetim** tarayıcı sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="1a432-196">Return to the **Cisco Cloud Collaboration Management** browser tab.</span></span> <span data-ttu-id="1a432-197">Test başarılı olduysa, seçin **bu test başarılı oldu. Çoklu oturum açma seçeneği etkinleştirme** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1a432-197">If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="1a432-198">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="1a432-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1a432-199">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="1a432-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1a432-200">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a432-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a432-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a432-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a432-202">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="1a432-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="1a432-204">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1a432-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1a432-205">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1a432-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a432-207">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="1a432-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a432-209">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="1a432-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a432-211">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1a432-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a432-213">a.</span><span class="sxs-lookup"><span data-stu-id="1a432-213">a.</span></span> <span data-ttu-id="1a432-214">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a432-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a432-215">b.</span><span class="sxs-lookup"><span data-stu-id="1a432-215">b.</span></span> <span data-ttu-id="1a432-216">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="1a432-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a432-217">c.</span><span class="sxs-lookup"><span data-stu-id="1a432-217">c.</span></span> <span data-ttu-id="1a432-218">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="1a432-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1a432-219">d.</span><span class="sxs-lookup"><span data-stu-id="1a432-219">d.</span></span> <span data-ttu-id="1a432-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1a432-220">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="1a432-221">Cisco Spark test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a432-221">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="1a432-222">Bu bölümde, Cisco Spark Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1a432-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="1a432-223">Bu bölümde, Cisco Spark Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1a432-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="1a432-224">Git [Cisco bulut işbirliği Yönetimi](https://admin.ciscospark.com/) tam yönetici kimlik bilgilerinizle.</span><span class="sxs-lookup"><span data-stu-id="1a432-224">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="1a432-225">Tıklatın **kullanıcılar** ve ardından **kullanıcıları yönetme**.</span><span class="sxs-lookup"><span data-stu-id="1a432-225">Click **Users** and then **Manage Users**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="1a432-227">İçinde **yönetmek kullanıcı** penceresinde, seçin **el ile ekleyin veya kullanıcıları değiştirin** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1a432-227">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="1a432-228">Seçin **adlarını ve e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="1a432-228">Select **Names and Email address**.</span></span> <span data-ttu-id="1a432-229">Ardından, metin kutusu aşağıdaki gibi doldurun:</span><span class="sxs-lookup"><span data-stu-id="1a432-229">Then, fill out the textbox as follows:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="1a432-231">a.</span><span class="sxs-lookup"><span data-stu-id="1a432-231">a.</span></span> <span data-ttu-id="1a432-232">İçinde **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1a432-232">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="1a432-233">b.</span><span class="sxs-lookup"><span data-stu-id="1a432-233">b.</span></span> <span data-ttu-id="1a432-234">İçinde **Soyadı** metin kutusuna, türü **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1a432-234">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="1a432-235">c.</span><span class="sxs-lookup"><span data-stu-id="1a432-235">c.</span></span> <span data-ttu-id="1a432-236">İçinde **e-posta adresi** metin kutusuna, türü  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1a432-236">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="1a432-237">Britta Simon eklemek için artı işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1a432-237">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="1a432-238">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1a432-238">Then, click **Next**.</span></span>

6. <span data-ttu-id="1a432-239">İçinde **Hizmetleri kullanıcıları eklemek** penceresinde tıklatın **kaydetmek** ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="1a432-239">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1a432-240">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="1a432-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1a432-241">Bu bölümde, Cisco Spark erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1a432-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="1a432-243">**Cisco Spark Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1a432-243">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="1a432-244">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1a432-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1a432-246">Uygulamalar listesinde **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="1a432-246">In the applications list, select **Cisco Spark**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="1a432-248">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1a432-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="1a432-250">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1a432-250">Click **Add** button.</span></span> <span data-ttu-id="1a432-251">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1a432-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="1a432-253">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1a432-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1a432-254">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1a432-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a432-255">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1a432-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a432-256">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1a432-256">Testing single sign-on</span></span>

<span data-ttu-id="1a432-257">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="1a432-257">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1a432-258">Erişim paneli Cisco Spark parçasında tıklattığınızda, otomatik olarak Cisco Spark uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="1a432-258">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a432-259">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1a432-259">Additional resources</span></span>

* [<span data-ttu-id="1a432-260">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="1a432-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a432-261">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1a432-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

