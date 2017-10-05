---
title: "Öğretici: Azure Active Directory Tümleştirme ile Printix | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Printix arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 97dbb3fa0531f2f679badb6bb9752f2e42fc9cb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="fbf84-103">Öğretici: Azure Active Directory Tümleştirme Printix ile</span><span class="sxs-lookup"><span data-stu-id="fbf84-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="fbf84-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Printix tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fbf84-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbf84-105">Printix Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fbf84-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fbf84-106">Printix erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fbf84-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="fbf84-107">Otomatik olarak için Printix (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fbf84-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbf84-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="fbf84-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fbf84-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbf84-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbf84-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fbf84-110">Prerequisites</span></span>

<span data-ttu-id="fbf84-111">Azure AD tümleştirme Printix ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbf84-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="fbf84-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fbf84-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbf84-113">Bir Printix çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="fbf84-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbf84-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fbf84-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbf84-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbf84-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbf84-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fbf84-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbf84-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbf84-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbf84-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fbf84-118">Scenario description</span></span>
<span data-ttu-id="fbf84-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fbf84-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbf84-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fbf84-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbf84-121">Galeriden Printix ekleme</span><span class="sxs-lookup"><span data-stu-id="fbf84-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="fbf84-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fbf84-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="fbf84-123">Galeriden Printix ekleme</span><span class="sxs-lookup"><span data-stu-id="fbf84-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="fbf84-124">Azure AD Printix tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Printix eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbf84-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fbf84-125">**Galeriden Printix eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbf84-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fbf84-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fbf84-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbf84-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fbf84-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="fbf84-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf84-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="fbf84-133">Arama kutusuna **Printix**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-133">In the search box, type **Printix**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="fbf84-135">Sonuçlar panelinde seçin **Printix**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf84-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbf84-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fbf84-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbf84-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Printix sınayın.</span><span class="sxs-lookup"><span data-stu-id="fbf84-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbf84-139">Tekli çalışmaya oturum için Azure AD Printix karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="fbf84-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="fbf84-140">Diğer bir deyişle, bir Azure AD kullanıcısının Printix ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbf84-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="fbf84-141">Printix içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="fbf84-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fbf84-142">Yapılandırma ve Azure AD çoklu oturum açma Printix ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbf84-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fbf84-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fbf84-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fbf84-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="fbf84-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbf84-145">**[Printix test kullanıcısı oluşturma](#creating-a-printix-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Printix sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="fbf84-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbf84-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fbf84-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbf84-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fbf84-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbf84-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fbf84-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbf84-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Printix uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fbf84-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="fbf84-150">**Azure AD çoklu oturum açma ile Printix yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbf84-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="fbf84-151">Azure portalında üzerinde **Printix** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="fbf84-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fbf84-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="fbf84-155">Üzerinde **Printix etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbf84-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="fbf84-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="fbf84-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbf84-158">Değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="fbf84-158">The value is not real.</span></span> <span data-ttu-id="fbf84-159">Değerin gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="fbf84-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="fbf84-160">Kişi [Printix istemci destek ekibi](mailto:support@printix.net) değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="fbf84-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
4. <span data-ttu-id="fbf84-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fbf84-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="fbf84-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf84-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbf84-165">Printix kiracınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="fbf84-165">Sign-on to your Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="fbf84-166">Üstteki menüde sağ üst köşesinde simgesini tıklatın ve seçin "**kimlik doğrulaması**".</span><span class="sxs-lookup"><span data-stu-id="fbf84-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="fbf84-168">Üzerinde **Kurulum** sekmesine **etkinleştirmek Azure/Office 365 kimlik doğrulaması**</span><span class="sxs-lookup"><span data-stu-id="fbf84-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="fbf84-170">Üzerinde **Azure** sekmesinde, metin kutusuna Federasyon meta verileri URL'sine Giriş "**Federasyon meta veri belgesi**".</span><span class="sxs-lookup"><span data-stu-id="fbf84-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="fbf84-171">Azure AD'den indirilen meta veri xml dosyası ekleme [Printix destek ekibi](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="fbf84-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="fbf84-172">Ardından xml dosyasını karşıya yüklemek ve Federasyon meta veri URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="fbf84-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="fbf84-174">Tıklayın "**Test**"düğmesini tıklatın ve tıklatın"**Tamam**" testi başarılı olursa düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf84-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="fbf84-175">Azure active directory sayfasında tıkladıktan sonra gösterilir **test** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf84-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="fbf84-176">"Test başarılı oldu" Buraya pop Azure test hesabınız kimlik bilgilerini girdikten sonra bir iletiyi "test Tamam ayarları" anlamına gelir. Ardından **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf84-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="fbf84-178">Tıklatın **kaydetmek** düğmesini "**kimlik doğrulaması**" sayfası.</span><span class="sxs-lookup"><span data-stu-id="fbf84-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="fbf84-179">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fbf84-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fbf84-180">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="fbf84-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fbf84-181">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbf84-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbf84-182">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbf84-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbf84-183">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="fbf84-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="fbf84-185">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbf84-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fbf84-186">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fbf84-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbf84-188">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbf84-190">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="fbf84-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbf84-192">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbf84-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbf84-194">a.</span><span class="sxs-lookup"><span data-stu-id="fbf84-194">a.</span></span> <span data-ttu-id="fbf84-195">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbf84-196">b.</span><span class="sxs-lookup"><span data-stu-id="fbf84-196">b.</span></span> <span data-ttu-id="fbf84-197">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="fbf84-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbf84-198">c.</span><span class="sxs-lookup"><span data-stu-id="fbf84-198">c.</span></span> <span data-ttu-id="fbf84-199">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fbf84-200">d.</span><span class="sxs-lookup"><span data-stu-id="fbf84-200">d.</span></span> <span data-ttu-id="fbf84-201">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbf84-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="fbf84-202">Printix test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbf84-202">Creating a Printix test user</span></span>

<span data-ttu-id="fbf84-203">Bu bölümün amacı Britta Simon içinde Printix adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="fbf84-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="fbf84-204">Printix yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="fbf84-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fbf84-205">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="fbf84-205">There is no action item for you in this section.</span></span> <span data-ttu-id="fbf84-206">Yeni bir kullanıcı henüz yoksa Printix erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fbf84-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="fbf84-207">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [Printix destek ekibi](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="fbf84-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fbf84-208">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="fbf84-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fbf84-209">Bu bölümde, Britta Printix için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fbf84-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="fbf84-211">**Printix için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbf84-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="fbf84-212">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fbf84-214">Uygulamalar listesinde **Printix**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-214">In the applications list, select **Printix**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="fbf84-216">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fbf84-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="fbf84-218">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbf84-218">Click **Add** button.</span></span> <span data-ttu-id="fbf84-219">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbf84-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="fbf84-221">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fbf84-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fbf84-222">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbf84-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbf84-223">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbf84-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbf84-224">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fbf84-224">Testing single sign-on</span></span>

<span data-ttu-id="fbf84-225">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="fbf84-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fbf84-226">Erişim paneli Printix parçasında tıklattığınızda, otomatik olarak Printix uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="fbf84-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbf84-227">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fbf84-227">Additional resources</span></span>

* [<span data-ttu-id="fbf84-228">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="fbf84-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbf84-229">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fbf84-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

