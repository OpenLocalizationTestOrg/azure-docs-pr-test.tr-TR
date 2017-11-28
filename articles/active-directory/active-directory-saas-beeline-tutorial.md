---
title: "Öğretici: Azure Active Directory Tümleştirme ile BeeLine | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile BeeLine arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 93acbd90bbe5f0a40bf3f56edb766a0fdd30f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="8ccb2-103">Öğretici: Azure Active Directory Tümleştirme BeeLine ile</span><span class="sxs-lookup"><span data-stu-id="8ccb2-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="8ccb2-104">Bu öğreticide, Azure Active Directory (Azure AD) ile BeeLine tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ccb2-105">BeeLine Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8ccb2-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8ccb2-106">BeeLine erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8ccb2-106">You can control in Azure AD who has access to BeeLine</span></span>
- <span data-ttu-id="8ccb2-107">Otomatik olarak için BeeLine (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8ccb2-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ccb2-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="8ccb2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8ccb2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ccb2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ccb2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8ccb2-110">Prerequisites</span></span>

<span data-ttu-id="8ccb2-111">Azure AD tümleştirme BeeLine ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="8ccb2-111">To configure Azure AD integration with BeeLine, you need the following items:</span></span>

- <span data-ttu-id="8ccb2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8ccb2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ccb2-113">Bir BeeLine çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="8ccb2-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ccb2-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ccb2-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8ccb2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ccb2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ccb2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ccb2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ccb2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8ccb2-118">Scenario description</span></span>
<span data-ttu-id="8ccb2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ccb2-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8ccb2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ccb2-121">Galeriden BeeLine ekleme</span><span class="sxs-lookup"><span data-stu-id="8ccb2-121">Adding BeeLine from the gallery</span></span>
2. <span data-ttu-id="8ccb2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8ccb2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="8ccb2-123">Galeriden BeeLine ekleme</span><span class="sxs-lookup"><span data-stu-id="8ccb2-123">Adding BeeLine from the gallery</span></span>
<span data-ttu-id="8ccb2-124">Azure AD BeeLine tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden BeeLine eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8ccb2-125">**Galeriden BeeLine eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8ccb2-125">**To add BeeLine from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8ccb2-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8ccb2-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8ccb2-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="8ccb2-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="8ccb2-133">Arama kutusuna **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-133">In the search box, type **BeeLine**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="8ccb2-135">Sonuçlar panelinde seçin **BeeLine**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ccb2-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8ccb2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ccb2-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı BeeLine ile test etme</span><span class="sxs-lookup"><span data-stu-id="8ccb2-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8ccb2-139">Tekli çalışmaya oturum için Azure AD BeeLine karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span></span> <span data-ttu-id="8ccb2-140">Diğer bir deyişle, bir Azure AD kullanıcısının BeeLine ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span></span>

<span data-ttu-id="8ccb2-141">BeeLine içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8ccb2-142">Yapılandırma ve Azure AD çoklu oturum açma BeeLine ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8ccb2-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8ccb2-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8ccb2-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ccb2-145">**[BeeLine test kullanıcısı oluşturma](#creating-a-beeline-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı BeeLine sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ccb2-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ccb2-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ccb2-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8ccb2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ccb2-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma BeeLine uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="8ccb2-150">**Azure AD çoklu oturum açma ile BeeLine yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8ccb2-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="8ccb2-151">Azure portalında üzerinde **BeeLine** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="8ccb2-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="8ccb2-155">Üzerinde **BeeLine etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8ccb2-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="8ccb2-157">a.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-157">a.</span></span> <span data-ttu-id="8ccb2-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="8ccb2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="8ccb2-159">b.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-159">b.</span></span> <span data-ttu-id="8ccb2-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="8ccb2-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="8ccb2-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-161">These values are not real.</span></span> <span data-ttu-id="8ccb2-162">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="8ccb2-163">Kişi [BeeLine destek ekibi](https://www.beeline.com/contact-us/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span></span>
 
4. <span data-ttu-id="8ccb2-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="8ccb2-166">Beeline uygulamanızı belirli bir biçimde SAML onaylar bekliyor.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-166">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8ccb2-167">Lütfen çalışmak [BeeLine destek ekibi](https://www.beeline.com/contact-us/) uygulamasına eşlenen doğru kullanıcı tanımlayıcısı belirlemek için öncelikle.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="8ccb2-168">Ayrıca Lütfen rehberliği almak [BeeLine destek ekibi](https://www.beeline.com/contact-us/) Bu eşleme için kullanmak istediğiniz özniteliği hakkında.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="8ccb2-169">Bu özniteliği değeri yönetebilirsiniz **kullanıcı öznitelikleri** uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span></span> <span data-ttu-id="8ccb2-170">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-170">The following screenshot shows an example for this.</span></span> <span data-ttu-id="8ccb2-171">Biz burada eşledikten **kullanıcı tanımlayıcısı** ile talep **userprincipalname** her başarılı SAML yanıt Beeline uygulamaya gönderilen benzersiz kullanıcı Kimliğini sağlar özniteliği.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="8ccb2-173">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-173">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8ccb2-175">Üzerinde **BeeLine yapılandırma** 'yi tıklatın **yapılandırma BeeLine** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8ccb2-176">Kopya **Sign-Out URL** ve **SAML varlık kimliği** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="8ccb2-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="8ccb2-178">Çoklu oturum açma yapılandırmak için **BeeLine** yan, indirilen göndermek için ihtiyacınız **meta veri XML** ve **SAML varlık kimliği**, **Sign-Out URL** için [BeeLine destek ekibi](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="8ccb2-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="8ccb2-179">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="8ccb2-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8ccb2-180">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8ccb2-181">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ccb2-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ccb2-182">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ccb2-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ccb2-183">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="8ccb2-185">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8ccb2-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8ccb2-186">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ccb2-188">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ccb2-190">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ccb2-192">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8ccb2-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ccb2-194">a.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-194">a.</span></span> <span data-ttu-id="8ccb2-195">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ccb2-196">b.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-196">b.</span></span> <span data-ttu-id="8ccb2-197">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ccb2-198">c.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-198">c.</span></span> <span data-ttu-id="8ccb2-199">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8ccb2-200">d.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-200">d.</span></span> <span data-ttu-id="8ccb2-201">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="8ccb2-202">BeeLine test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ccb2-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="8ccb2-203">Bu bölümde, Beeline içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="8ccb2-204">Beeline uygulamanın tüm kullanıcılar tekli oturum açma işleminden önce uygulamayı sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="8ccb2-205">Böylece iş [BeeLine destek ekibi](https://www.beeline.com/contact-us/) bu kullanıcıların uygulamaya sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8ccb2-206">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="8ccb2-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8ccb2-207">Bu bölümde, Britta BeeLine için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8ccb2-209">**BeeLine için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8ccb2-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="8ccb2-210">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8ccb2-212">Uygulamalar listesinde **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-212">In the applications list, select **BeeLine**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="8ccb2-214">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="8ccb2-216">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-216">Click **Add** button.</span></span> <span data-ttu-id="8ccb2-217">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="8ccb2-219">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8ccb2-220">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ccb2-221">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ccb2-222">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8ccb2-222">Testing single sign-on</span></span>

<span data-ttu-id="8ccb2-223">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="8ccb2-224">Erişim paneli Beeline parçasında tıklattığınızda, otomatik olarak Beeline uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="8ccb2-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ccb2-225">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8ccb2-225">Additional resources</span></span>

* [<span data-ttu-id="8ccb2-226">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="8ccb2-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ccb2-227">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8ccb2-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

