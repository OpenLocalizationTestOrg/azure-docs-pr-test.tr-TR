---
title: "Öğretici: Azure Active Directory Tümleştirme ile Wingspan eTMF | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Wingspan eTMF arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 8c76fb64229abcad0cabb910e7c170979a79d839
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="febe3-103">Öğretici: Azure Active Directory Tümleştirme Wingspan eTMF ile</span><span class="sxs-lookup"><span data-stu-id="febe3-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="febe3-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Wingspan eTMF tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="febe3-104">In this tutorial, you learn how to integrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="febe3-105">Wingspan eTMF Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="febe3-105">Integrating Wingspan eTMF with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="febe3-106">Wingspan eTMF erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="febe3-106">You can control in Azure AD who has access to Wingspan eTMF</span></span>
- <span data-ttu-id="febe3-107">Otomatik olarak Azure AD hesaplarına sahip Wingspan eTMF (çoklu oturum açma) için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="febe3-107">You can enable your users to automatically get signed-on to Wingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="febe3-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="febe3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="febe3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="febe3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="febe3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="febe3-110">Prerequisites</span></span>

<span data-ttu-id="febe3-111">Azure AD tümleştirme Wingspan eTMF ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="febe3-111">To configure Azure AD integration with Wingspan eTMF, you need the following items:</span></span>

- <span data-ttu-id="febe3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="febe3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="febe3-113">Bir Wingspan eTMF çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="febe3-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="febe3-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="febe3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="febe3-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="febe3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="febe3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="febe3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="febe3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="febe3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="febe3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="febe3-118">Scenario description</span></span>
<span data-ttu-id="febe3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="febe3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="febe3-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="febe3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="febe3-121">Galeriden Wingspan eTMF ekleme</span><span class="sxs-lookup"><span data-stu-id="febe3-121">Adding Wingspan eTMF from the gallery</span></span>
2. <span data-ttu-id="febe3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="febe3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-the-gallery"></a><span data-ttu-id="febe3-123">Galeriden Wingspan eTMF ekleme</span><span class="sxs-lookup"><span data-stu-id="febe3-123">Adding Wingspan eTMF from the gallery</span></span>
<span data-ttu-id="febe3-124">Azure AD Wingspan eTMF tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Wingspan eTMF eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="febe3-124">To configure the integration of Wingspan eTMF into Azure AD, you need to add Wingspan eTMF from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="febe3-125">**Galeriden Wingspan eTMF eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="febe3-125">**To add Wingspan eTMF from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="febe3-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="febe3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="febe3-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="febe3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="febe3-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="febe3-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="febe3-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="febe3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="febe3-133">Arama kutusuna **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="febe3-133">In the search box, type **Wingspan eTMF**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

5. <span data-ttu-id="febe3-135">Sonuçlar panelinde seçin **Wingspan eTMF**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="febe3-135">In the results panel, select **Wingspan eTMF**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="febe3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="febe3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="febe3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Wingspan eTMF ile test etme</span><span class="sxs-lookup"><span data-stu-id="febe3-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="febe3-139">Tekli çalışmaya oturum için Azure AD Wingspan eTMF karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="febe3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wingspan eTMF is to a user in Azure AD.</span></span> <span data-ttu-id="febe3-140">Diğer bir deyişle, bir Azure AD kullanıcısının Wingspan eTMF ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="febe3-140">In other words, a link relationship between an Azure AD user and the related user in Wingspan eTMF needs to be established.</span></span>

<span data-ttu-id="febe3-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Wingspan eTMF içinde.</span><span class="sxs-lookup"><span data-stu-id="febe3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="febe3-142">Yapılandırma ve Azure AD çoklu oturum açma Wingspan eTMF ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="febe3-142">To configure and test Azure AD single sign-on with Wingspan eTMF, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="febe3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="febe3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="febe3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="febe3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="febe3-145">**[Wingspan eTMF test kullanıcısı oluşturma](#creating-a-wingspan-etmf-test-user)**  - bir Britta Simon karşılık gelen kullanıcı Azure AD gösterimini bağlı Wingspan eTMF içinde olması.</span><span class="sxs-lookup"><span data-stu-id="febe3-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - to have a counterpart of Britta Simon in Wingspan eTMF that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="febe3-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="febe3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="febe3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="febe3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="febe3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="febe3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="febe3-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Wingspan eTMF uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="febe3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="febe3-150">**Azure AD çoklu oturum açma Wingspan eTMF ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="febe3-150">**To configure Azure AD single sign-on with Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="febe3-151">Azure portalında üzerinde **Wingspan eTMF** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="febe3-151">In the Azure portal, on the **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="febe3-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="febe3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

3. <span data-ttu-id="febe3-155">Üzerinde **Wingspan eTMF etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="febe3-155">On the **Wingspan eTMF Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="febe3-157">a.</span><span class="sxs-lookup"><span data-stu-id="febe3-157">a.</span></span> <span data-ttu-id="febe3-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<customer name>.<instance name>.mywingspan.com/saml`</span><span class="sxs-lookup"><span data-stu-id="febe3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="febe3-159">b.</span><span class="sxs-lookup"><span data-stu-id="febe3-159">b.</span></span> <span data-ttu-id="febe3-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="febe3-160">In the **Identifier** textbox, type a URL using the following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="febe3-161">c.</span><span class="sxs-lookup"><span data-stu-id="febe3-161">c.</span></span> <span data-ttu-id="febe3-162">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<customer name>.<instance name>.mywingspan.com/`</span><span class="sxs-lookup"><span data-stu-id="febe3-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="febe3-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="febe3-163">These values are not the real.</span></span> <span data-ttu-id="febe3-164">Bu değerleri gerçek oturum açma URL'si, tanımlayıcı ve yanıt gerçek müşteri adı ve örnek adı dahil olmak üzere URL ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="febe3-164">Update these values with the actual Sign-On URL, Identifier and Reply URL including the actual customer name and instance name.</span></span> <span data-ttu-id="febe3-165">Kişi [Wingspan eTMF istemci destek ekibi](http://www.wingspan.com/contact-us/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="febe3-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="febe3-166">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="febe3-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

5. <span data-ttu-id="febe3-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="febe3-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="febe3-170">Çoklu oturum açma yapılandırmak için **Wingspan eTMF** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [Wingspan eTMF Destek](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="febe3-170">To configure single sign-on on **Wingspan eTMF** side, you need to send the downloaded **Metadata XML** to [Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="febe3-171">Bunlar bu iki tarafta da ayarlamanızı SAML SSO bağlantınız şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="febe3-171">They set this up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="febe3-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="febe3-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="febe3-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="febe3-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="febe3-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="febe3-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="febe3-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="febe3-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="febe3-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="febe3-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="febe3-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="febe3-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="febe3-179">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="febe3-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="febe3-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="febe3-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="febe3-183">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="febe3-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="febe3-185">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="febe3-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="febe3-187">a.</span><span class="sxs-lookup"><span data-stu-id="febe3-187">a.</span></span> <span data-ttu-id="febe3-188">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="febe3-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="febe3-189">b.</span><span class="sxs-lookup"><span data-stu-id="febe3-189">b.</span></span> <span data-ttu-id="febe3-190">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="febe3-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="febe3-191">c.</span><span class="sxs-lookup"><span data-stu-id="febe3-191">c.</span></span> <span data-ttu-id="febe3-192">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="febe3-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="febe3-193">d.</span><span class="sxs-lookup"><span data-stu-id="febe3-193">d.</span></span> <span data-ttu-id="febe3-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="febe3-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="febe3-195">Wingspan eTMF test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="febe3-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="febe3-196">Bu bölümde, Britta Simon Wingspan eTMF adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="febe3-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="febe3-197">Çalışmak [Wingspan eTMF Destek](http://www.wingspan.com/contact-us/) Wingspan eTMF uygulamada kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="febe3-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) to add the users in the Wingspan eTMF application.</span></span> <span data-ttu-id="febe3-198">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="febe3-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="febe3-199">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="febe3-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="febe3-200">Bu bölümde, Britta Wingspan eTMF erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="febe3-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wingspan eTMF.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="febe3-202">**Wingspan eTMF Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="febe3-202">**To assign Britta Simon to Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="febe3-203">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="febe3-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="febe3-205">Uygulamalar listesinde **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="febe3-205">In the applications list, select **Wingspan eTMF**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

3. <span data-ttu-id="febe3-207">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="febe3-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="febe3-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="febe3-209">Click **Add** button.</span></span> <span data-ttu-id="febe3-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="febe3-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="febe3-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="febe3-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="febe3-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="febe3-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="febe3-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="febe3-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="febe3-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="febe3-215">Testing single sign-on</span></span>

<span data-ttu-id="febe3-216">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="febe3-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="febe3-217">Erişim panelinde Wingspan eTMF kutucuğuna tıklayın, kuruluşunuzun oturum açma sayfası için yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="febe3-217">Click the Wingspan eTMF tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="febe3-218">Başarılı oturum açtıktan sonra Wingspan eTMF uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="febe3-218">After successful login, you will be signed-on to your Wingspan eTMF application.</span></span> <span data-ttu-id="febe3-219">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="febe3-219">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="febe3-220">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="febe3-220">Additional resources</span></span>

* [<span data-ttu-id="febe3-221">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="febe3-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="febe3-222">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="febe3-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_203.png

