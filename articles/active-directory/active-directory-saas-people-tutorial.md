---
title: "Öğretici: Azure Active Directory Tümleştirme kişilerle | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve kişiler arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: caa287a2ed8774965ef722685e4e950336e5e0ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="460f3-103">Öğretici: Azure Active Directory Tümleştirme kişilerle</span><span class="sxs-lookup"><span data-stu-id="460f3-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="460f3-104">Bu öğreticide, Azure Active Directory (Azure AD) ile kişiler tümleştirin öğrenin.</span><span class="sxs-lookup"><span data-stu-id="460f3-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="460f3-105">Kişilerin Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="460f3-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="460f3-106">Kişilerin erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="460f3-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="460f3-107">Otomatik olarak kişilere (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="460f3-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="460f3-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="460f3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="460f3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="460f3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="460f3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="460f3-110">Prerequisites</span></span>

<span data-ttu-id="460f3-111">Azure AD tümleştirme kişilerle yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="460f3-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="460f3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="460f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="460f3-113">Bir kişi çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="460f3-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="460f3-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="460f3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="460f3-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="460f3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="460f3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="460f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="460f3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="460f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="460f3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="460f3-118">Scenario description</span></span>
<span data-ttu-id="460f3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="460f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="460f3-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="460f3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="460f3-121">Galeriden kişiler ekleme</span><span class="sxs-lookup"><span data-stu-id="460f3-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="460f3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="460f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="460f3-123">Galeriden kişiler ekleme</span><span class="sxs-lookup"><span data-stu-id="460f3-123">Adding People from the gallery</span></span>
<span data-ttu-id="460f3-124">Azure AD kişiler tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden kişiler eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="460f3-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="460f3-125">**Galeriden kişileri eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="460f3-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="460f3-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="460f3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="460f3-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="460f3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="460f3-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="460f3-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="460f3-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="460f3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="460f3-133">Arama kutusuna **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="460f3-133">In the search box, type **People**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="460f3-135">Sonuçlar panelinde seçin **kişiler**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="460f3-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="460f3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="460f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="460f3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı kişilerle test etme.</span><span class="sxs-lookup"><span data-stu-id="460f3-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="460f3-139">Tekli çalışmaya oturum için Azure AD kişiler karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="460f3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="460f3-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı kişiler arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="460f3-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="460f3-141">Değeri, kişilere atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="460f3-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="460f3-142">Yapılandırmak ve Azure AD çoklu oturum açma kişilerle sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="460f3-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="460f3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="460f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="460f3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="460f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="460f3-145">**[Kişiler test kullanıcısı oluşturma](#creating-a-people-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlantılı Kişiler sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="460f3-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="460f3-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="460f3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="460f3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="460f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="460f3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="460f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="460f3-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma kişiler uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="460f3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="460f3-150">**Azure AD çoklu oturum açma kişilerle yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="460f3-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="460f3-151">Azure portalında üzerinde **kişiler** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="460f3-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="460f3-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="460f3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="460f3-155">Üzerinde **kişiler etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="460f3-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="460f3-157">a.</span><span class="sxs-lookup"><span data-stu-id="460f3-157">a.</span></span> <span data-ttu-id="460f3-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="460f3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="460f3-159">b.</span><span class="sxs-lookup"><span data-stu-id="460f3-159">b.</span></span> <span data-ttu-id="460f3-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="460f3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="460f3-161">c.</span><span class="sxs-lookup"><span data-stu-id="460f3-161">c.</span></span> <span data-ttu-id="460f3-162">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="460f3-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="460f3-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="460f3-163">These values are not real.</span></span> <span data-ttu-id="460f3-164">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="460f3-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="460f3-165">Kişi [kişiler istemci destek ekibi](mailto:customerservices@peoplehr.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="460f3-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span>

5. <span data-ttu-id="460f3-166">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="460f3-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="460f3-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="460f3-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="460f3-170">Uygulamanız için yapılandırılmış SSO almak için kişiler kiracınız yönetici olarak oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="460f3-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="460f3-171">Sol tarafındaki menüde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="460f3-171">In the menu on the left side, click **Settings**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="460f3-173">Tıklatın **şirket**.</span><span class="sxs-lookup"><span data-stu-id="460f3-173">Click **Company**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="460f3-175">Üzerinde **karşıya yükleme 'Single Sign tam On' SAML meta veri dosyası**, tıklatın **Gözat** indirilen meta veri dosyasını karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="460f3-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="460f3-177">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="460f3-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="460f3-178">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="460f3-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="460f3-179">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="460f3-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="460f3-180">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="460f3-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="460f3-181">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="460f3-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="460f3-183">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="460f3-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="460f3-184">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="460f3-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="460f3-186">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="460f3-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="460f3-188">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="460f3-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="460f3-190">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="460f3-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="460f3-192">a.</span><span class="sxs-lookup"><span data-stu-id="460f3-192">a.</span></span> <span data-ttu-id="460f3-193">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="460f3-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="460f3-194">b.</span><span class="sxs-lookup"><span data-stu-id="460f3-194">b.</span></span> <span data-ttu-id="460f3-195">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="460f3-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="460f3-196">c.</span><span class="sxs-lookup"><span data-stu-id="460f3-196">c.</span></span> <span data-ttu-id="460f3-197">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="460f3-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="460f3-198">d.</span><span class="sxs-lookup"><span data-stu-id="460f3-198">d.</span></span> <span data-ttu-id="460f3-199">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="460f3-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="460f3-200">Kişiler test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="460f3-200">Creating a People test user</span></span>

<span data-ttu-id="460f3-201">Bu bölümde, kişilerin Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="460f3-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="460f3-202">Çalışmak [kişiler istemci destek ekibi](mailto:customerservices@peoplehr.com) kişiler platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="460f3-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="460f3-203">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="460f3-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="460f3-204">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="460f3-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="460f3-205">Bu bölümde, Britta kişilere erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="460f3-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="460f3-207">**Kişilere Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="460f3-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="460f3-208">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="460f3-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="460f3-210">Uygulamalar listesinde **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="460f3-210">In the applications list, select **People**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="460f3-212">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="460f3-212">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="460f3-214">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="460f3-214">Click **Add** button.</span></span> <span data-ttu-id="460f3-215">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="460f3-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="460f3-217">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="460f3-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="460f3-218">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="460f3-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="460f3-219">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="460f3-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="460f3-220">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="460f3-220">Testing single sign-on</span></span>

<span data-ttu-id="460f3-221">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="460f3-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="460f3-222">Erişim paneli kişiler parçasında tıklattığınızda, otomatik olarak kişiler uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="460f3-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="460f3-223">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="460f3-223">Additional resources</span></span>

* [<span data-ttu-id="460f3-224">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="460f3-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="460f3-225">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="460f3-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

