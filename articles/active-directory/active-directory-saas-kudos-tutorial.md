---
title: "Öğretici: Azure Active Directory Tümleştirme ile Kudos | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Kudos arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 353798fcfd4ad7ce017fc2fddf4110715db3ace2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="391b5-103">Öğretici: Azure Active Directory Tümleştirme Kudos ile</span><span class="sxs-lookup"><span data-stu-id="391b5-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="391b5-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Kudos tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="391b5-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="391b5-105">Kudos Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="391b5-105">Integrating Kudos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="391b5-106">Kudos erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="391b5-106">You can control in Azure AD who has access to Kudos</span></span>
- <span data-ttu-id="391b5-107">Otomatik olarak için Kudos (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="391b5-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="391b5-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="391b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="391b5-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="391b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="391b5-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="391b5-110">Prerequisites</span></span>

<span data-ttu-id="391b5-111">Azure AD tümleştirme Kudos ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="391b5-111">To configure Azure AD integration with Kudos, you need the following items:</span></span>

- <span data-ttu-id="391b5-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="391b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="391b5-113">Bir Kudos çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="391b5-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="391b5-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="391b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="391b5-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="391b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="391b5-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="391b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="391b5-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="391b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="391b5-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="391b5-118">Scenario description</span></span>
<span data-ttu-id="391b5-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="391b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="391b5-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="391b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="391b5-121">Galeriden Kudos ekleme</span><span class="sxs-lookup"><span data-stu-id="391b5-121">Adding Kudos from the gallery</span></span>
2. <span data-ttu-id="391b5-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="391b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-the-gallery"></a><span data-ttu-id="391b5-123">Galeriden Kudos ekleme</span><span class="sxs-lookup"><span data-stu-id="391b5-123">Adding Kudos from the gallery</span></span>
<span data-ttu-id="391b5-124">Azure AD Kudos tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Kudos eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="391b5-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="391b5-125">**Galeriden Kudos eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="391b5-125">**To add Kudos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="391b5-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="391b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="391b5-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="391b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="391b5-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="391b5-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="391b5-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="391b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="391b5-133">Arama kutusuna **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="391b5-133">In the search box, type **Kudos**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="391b5-135">Sonuçlar panelinde seçin **Kudos**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="391b5-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="391b5-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="391b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="391b5-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Kudos sınayın.</span><span class="sxs-lookup"><span data-stu-id="391b5-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="391b5-139">Tekli çalışmaya oturum için Azure AD Kudos karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="391b5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span></span> <span data-ttu-id="391b5-140">Diğer bir deyişle, bir Azure AD kullanıcısının Kudos ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="391b5-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span></span>

<span data-ttu-id="391b5-141">Kudos içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="391b5-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="391b5-142">Yapılandırma ve Azure AD çoklu oturum açma Kudos ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="391b5-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="391b5-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="391b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="391b5-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="391b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="391b5-145">**[Kudos test kullanıcısı oluşturma](#creating-a-kudos-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Kudos sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="391b5-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="391b5-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="391b5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="391b5-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="391b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="391b5-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="391b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="391b5-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Kudos uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="391b5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="391b5-150">**Azure AD çoklu oturum açma ile Kudos yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="391b5-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="391b5-151">Azure portalında üzerinde **Kudos** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="391b5-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="391b5-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="391b5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="391b5-155">Üzerinde **Kudos etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="391b5-155">On the **Kudos Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="391b5-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="391b5-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="391b5-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="391b5-158">This value is not real.</span></span> <span data-ttu-id="391b5-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="391b5-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="391b5-160">Kişi [Kudos istemci destek ekibi](http://success.kudosnow.com/home) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="391b5-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span></span> 
 
4. <span data-ttu-id="391b5-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="391b5-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="391b5-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="391b5-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="391b5-165">Üzerinde **Kudos yapılandırma** 'yi tıklatın **yapılandırma Kudos** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="391b5-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span></span> <span data-ttu-id="391b5-166">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="391b5-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="391b5-168">Farklı web tarayıcısı penceresinde Kudos şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="391b5-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="391b5-169">Üstteki menüde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="391b5-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="391b5-170">![Ayarları](./media/active-directory-saas-kudos-tutorial/ic787806.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="391b5-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="391b5-171">Tıklatın **tümleştirmeler \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="391b5-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="391b5-172">İçinde **SSO** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="391b5-172">In the **SSO** section, perform the following steps:</span></span>
   
    <span data-ttu-id="391b5-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="391b5-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="391b5-174">a.</span><span class="sxs-lookup"><span data-stu-id="391b5-174">a.</span></span> <span data-ttu-id="391b5-175">İçinde **URL üzerinde oturum** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="391b5-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="391b5-176">b.</span><span class="sxs-lookup"><span data-stu-id="391b5-176">b.</span></span> <span data-ttu-id="391b5-177">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **X.509 sertifikası** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="391b5-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="391b5-178">c.</span><span class="sxs-lookup"><span data-stu-id="391b5-178">c.</span></span> <span data-ttu-id="391b5-179">İçinde **oturum kapatma URL'si**, değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="391b5-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="391b5-180">d.</span><span class="sxs-lookup"><span data-stu-id="391b5-180">d.</span></span> <span data-ttu-id="391b5-181">İçinde **Kudos URL'niz** metin kutusuna, şirketinizin adını yazın.</span><span class="sxs-lookup"><span data-stu-id="391b5-181">In the **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="391b5-182">e.</span><span class="sxs-lookup"><span data-stu-id="391b5-182">e.</span></span> <span data-ttu-id="391b5-183">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="391b5-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="391b5-184">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="391b5-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="391b5-185">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="391b5-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="391b5-186">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="391b5-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="391b5-187">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="391b5-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="391b5-188">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="391b5-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="391b5-190">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="391b5-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="391b5-191">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="391b5-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="391b5-193">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="391b5-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="391b5-195">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="391b5-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="391b5-197">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="391b5-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="391b5-199">a.</span><span class="sxs-lookup"><span data-stu-id="391b5-199">a.</span></span> <span data-ttu-id="391b5-200">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="391b5-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="391b5-201">b.</span><span class="sxs-lookup"><span data-stu-id="391b5-201">b.</span></span> <span data-ttu-id="391b5-202">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="391b5-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="391b5-203">c.</span><span class="sxs-lookup"><span data-stu-id="391b5-203">c.</span></span> <span data-ttu-id="391b5-204">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="391b5-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="391b5-205">d.</span><span class="sxs-lookup"><span data-stu-id="391b5-205">d.</span></span> <span data-ttu-id="391b5-206">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="391b5-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="391b5-207">Kudos test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="391b5-207">Creating a Kudos test user</span></span>

<span data-ttu-id="391b5-208">Azure AD kullanıcıların Kudos oturum etkinleştirmek için bunların Kudos sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="391b5-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="391b5-209">Kudos söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="391b5-209">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="391b5-210">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="391b5-210">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="391b5-211">Oturum, **Kudos** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="391b5-211">Log in to your **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="391b5-212">Üstteki menüde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="391b5-212">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="391b5-213">![Ayarları](./media/active-directory-saas-kudos-tutorial/ic787806.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="391b5-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="391b5-214">Tıklatın **kullanıcı yönetici**.</span><span class="sxs-lookup"><span data-stu-id="391b5-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="391b5-215">Tıklatın **kullanıcılar** sekmesini ve ardından **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="391b5-215">Click the **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="391b5-216">![Kullanıcı Yönetim](./media/active-directory-saas-kudos-tutorial/ic787809.png "kullanıcı yönetici")</span><span class="sxs-lookup"><span data-stu-id="391b5-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="391b5-217">İçinde **kullanıcı ekleme** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="391b5-217">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="391b5-218">![Kullanıcı ekleme](./media/active-directory-saas-kudos-tutorial/ic787810.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="391b5-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="391b5-219">a.</span><span class="sxs-lookup"><span data-stu-id="391b5-219">a.</span></span> <span data-ttu-id="391b5-220">Tür **ad**, **Soyadı**, **e-posta** ve diğer ayrıntılarını istediğiniz ilgili metin kutularına sağlamayı geçerli bir Azure Active Directory hesabı.</span><span class="sxs-lookup"><span data-stu-id="391b5-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="391b5-221">b.</span><span class="sxs-lookup"><span data-stu-id="391b5-221">b.</span></span> <span data-ttu-id="391b5-222">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="391b5-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="391b5-223">API sağlama AAD kullanıcı hesaplarına Kudos tarafından sağlanan veya herhangi diğer Kudos kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="391b5-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="391b5-224">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="391b5-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="391b5-225">Bu bölümde, Britta Kudos için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="391b5-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="391b5-227">**Kudos için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="391b5-227">**To assign Britta Simon to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="391b5-228">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="391b5-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="391b5-230">Uygulamalar listesinde **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="391b5-230">In the applications list, select **Kudos**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="391b5-232">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="391b5-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="391b5-234">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="391b5-234">Click **Add** button.</span></span> <span data-ttu-id="391b5-235">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="391b5-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="391b5-237">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="391b5-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="391b5-238">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="391b5-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="391b5-239">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="391b5-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="391b5-240">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="391b5-240">Testing single sign-on</span></span>

<span data-ttu-id="391b5-241">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="391b5-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="391b5-242">Erişim paneli Kudos parçasında tıklattığınızda, otomatik olarak Kudos uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="391b5-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span></span> <span data-ttu-id="391b5-243">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="391b5-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="391b5-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="391b5-244">Additional resources</span></span>

* [<span data-ttu-id="391b5-245">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="391b5-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="391b5-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="391b5-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

