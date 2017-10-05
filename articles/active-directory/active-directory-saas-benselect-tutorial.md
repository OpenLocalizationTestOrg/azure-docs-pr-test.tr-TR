---
title: "Öğretici: Azure Active Directory Tümleştirme ile BenSelect | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile BenSelect arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: f8caa023da05863372b7ef92b47a92168445d741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="cd5df-103">Öğretici: Azure Active Directory Tümleştirme BenSelect ile</span><span class="sxs-lookup"><span data-stu-id="cd5df-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="cd5df-104">Bu öğreticide, Azure Active Directory (Azure AD) ile BenSelect tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="cd5df-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd5df-105">BenSelect Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cd5df-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cd5df-106">BenSelect erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cd5df-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="cd5df-107">Otomatik olarak için BenSelect (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cd5df-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd5df-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="cd5df-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cd5df-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cd5df-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd5df-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cd5df-110">Prerequisites</span></span>

<span data-ttu-id="cd5df-111">Azure AD tümleştirme BenSelect ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="cd5df-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="cd5df-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cd5df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd5df-113">Bir BenSelect çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="cd5df-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd5df-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cd5df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd5df-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cd5df-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd5df-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cd5df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd5df-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd5df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd5df-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cd5df-118">Scenario description</span></span>
<span data-ttu-id="cd5df-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cd5df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd5df-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cd5df-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd5df-121">Galeriden BenSelect ekleme</span><span class="sxs-lookup"><span data-stu-id="cd5df-121">Adding BenSelect from the gallery</span></span>
2. <span data-ttu-id="cd5df-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cd5df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="cd5df-123">Galeriden BenSelect ekleme</span><span class="sxs-lookup"><span data-stu-id="cd5df-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="cd5df-124">Azure AD BenSelect tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden BenSelect eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd5df-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cd5df-125">**Galeriden BenSelect eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cd5df-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cd5df-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cd5df-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cd5df-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cd5df-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="cd5df-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cd5df-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="cd5df-133">Arama kutusuna **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-133">In the search box, type **BenSelect**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="cd5df-135">Sonuçlar panelinde seçin **BenSelect**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cd5df-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd5df-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cd5df-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd5df-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BenSelect ile test etme</span><span class="sxs-lookup"><span data-stu-id="cd5df-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cd5df-139">Tekli çalışmaya oturum için Azure AD BenSelect karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="cd5df-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="cd5df-140">Diğer bir deyişle, bir Azure AD kullanıcısının BenSelect ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd5df-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="cd5df-141">BenSelect içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cd5df-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cd5df-142">Yapılandırma ve Azure AD çoklu oturum açma BenSelect ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cd5df-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cd5df-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cd5df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cd5df-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="cd5df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd5df-145">**[BenSelect test kullanıcısı oluşturma](#creating-a-benselect-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı BenSelect sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="cd5df-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd5df-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cd5df-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd5df-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cd5df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd5df-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cd5df-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd5df-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma BenSelect uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cd5df-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="cd5df-150">**Azure AD çoklu oturum açma ile BenSelect yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cd5df-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="cd5df-151">Azure portalında üzerinde **BenSelect** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="cd5df-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cd5df-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="cd5df-155">Üzerinde **BenSelect etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cd5df-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="cd5df-157">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="cd5df-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd5df-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="cd5df-158">This value is not real.</span></span> <span data-ttu-id="cd5df-159">Bu değer ile gerçek yanıt URL'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cd5df-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="cd5df-160">Kişi [BenSelect destek ekibi](mailto:support@selerix.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="cd5df-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
4. <span data-ttu-id="cd5df-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Raw)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cd5df-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="cd5df-163">BenSelect uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="cd5df-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="cd5df-164">Bu uygulama için aşağıdaki talep yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cd5df-164">Configure the following claims for this application.</span></span> <span data-ttu-id="cd5df-165">Bu öznitelik değerlerini yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="cd5df-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="cd5df-166">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="cd5df-166">The following screenshot shows an example for this.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="cd5df-168">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim:</span><span class="sxs-lookup"><span data-stu-id="cd5df-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="cd5df-169">a.</span><span class="sxs-lookup"><span data-stu-id="cd5df-169">a.</span></span> <span data-ttu-id="cd5df-170">İçinde **kullanıcı tanımlayıcısı** açılır listesinden, **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="cd5df-171">b.</span><span class="sxs-lookup"><span data-stu-id="cd5df-171">b.</span></span> <span data-ttu-id="cd5df-172">İçinde **posta** açılır listesinden, **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="cd5df-173">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cd5df-173">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cd5df-175">Üzerinde **BenSelect yapılandırma** 'yi tıklatın **yapılandırma BenSelect** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cd5df-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cd5df-176">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cd5df-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="cd5df-178">Çoklu oturum açma yapılandırmak için **BenSelect** yan, indirilen göndermek için ihtiyacınız **Certificate(Raw)** ve **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** için [BenSelect destek ekibi](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="cd5df-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="cd5df-179">Bu tümleştirme (SHA1 desteklenmez) SHA256 algoritmasını gerektirir anlatılması gerekir SSO app2101 gibi uygun sunucu vb. ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="cd5df-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="cd5df-180">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cd5df-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cd5df-181">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="cd5df-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cd5df-182">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cd5df-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd5df-183">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd5df-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd5df-184">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="cd5df-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="cd5df-186">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cd5df-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cd5df-187">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cd5df-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd5df-189">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd5df-191">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="cd5df-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd5df-193">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cd5df-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd5df-195">a.</span><span class="sxs-lookup"><span data-stu-id="cd5df-195">a.</span></span> <span data-ttu-id="cd5df-196">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd5df-197">b.</span><span class="sxs-lookup"><span data-stu-id="cd5df-197">b.</span></span> <span data-ttu-id="cd5df-198">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="cd5df-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd5df-199">c.</span><span class="sxs-lookup"><span data-stu-id="cd5df-199">c.</span></span> <span data-ttu-id="cd5df-200">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cd5df-201">d.</span><span class="sxs-lookup"><span data-stu-id="cd5df-201">d.</span></span> <span data-ttu-id="cd5df-202">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cd5df-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="cd5df-203">BenSelect test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd5df-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="cd5df-204">Bu bölümün amacı Britta Simon içinde BenSelect adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="cd5df-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="cd5df-205">Çalışmak [BenSelect destek ekibi](mailto:support@selerix.com) BenSelect hesap kullanıcılar eklemek için.</span><span class="sxs-lookup"><span data-stu-id="cd5df-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cd5df-206">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="cd5df-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cd5df-207">Bu bölümde, Britta BenSelect için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cd5df-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="cd5df-209">**BenSelect için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cd5df-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="cd5df-210">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cd5df-212">Uygulamalar listesinde **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-212">In the applications list, select **BenSelect**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="cd5df-214">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cd5df-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="cd5df-216">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cd5df-216">Click **Add** button.</span></span> <span data-ttu-id="cd5df-217">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cd5df-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="cd5df-219">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cd5df-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cd5df-220">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cd5df-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd5df-221">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cd5df-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cd5df-222">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cd5df-222">Testing single sign-on</span></span>

<span data-ttu-id="cd5df-223">Bu bölümde, erişim paneli kullanarak Azure AD SSO yapılandırmanızı sınayın.</span><span class="sxs-lookup"><span data-stu-id="cd5df-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="cd5df-224">Erişim paneli BenSelect parçasında tıklattığınızda, otomatik olarak BenSelect uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="cd5df-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd5df-225">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cd5df-225">Additional resources</span></span>

* [<span data-ttu-id="cd5df-226">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="cd5df-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd5df-227">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cd5df-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

