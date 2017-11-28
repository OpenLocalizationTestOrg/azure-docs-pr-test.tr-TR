---
title: "Öğretici: Azure Active Directory Tümleştirme ile StatusPage | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile StatusPage arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: fa16cdec7b89404c140435fe57d5aa4b08cfa985
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="1e8ac-103">Öğretici: Azure Active Directory Tümleştirme StatusPage ile</span><span class="sxs-lookup"><span data-stu-id="1e8ac-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="1e8ac-104">Bu öğreticide, Azure Active Directory (Azure AD) ile StatusPage tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e8ac-105">StatusPage Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e8ac-106">StatusPage erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1e8ac-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="1e8ac-107">Otomatik olarak için StatusPage (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1e8ac-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e8ac-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="1e8ac-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1e8ac-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e8ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e8ac-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1e8ac-110">Prerequisites</span></span>

<span data-ttu-id="1e8ac-111">Azure AD tümleştirme StatusPage ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="1e8ac-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1e8ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e8ac-113">Bir StatusPage çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="1e8ac-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e8ac-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e8ac-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e8ac-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e8ac-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e8ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e8ac-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1e8ac-118">Scenario description</span></span>
<span data-ttu-id="1e8ac-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e8ac-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e8ac-121">Galeriden StatusPage ekleme</span><span class="sxs-lookup"><span data-stu-id="1e8ac-121">Adding StatusPage from the gallery</span></span>
2. <span data-ttu-id="1e8ac-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1e8ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="1e8ac-123">Galeriden StatusPage ekleme</span><span class="sxs-lookup"><span data-stu-id="1e8ac-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="1e8ac-124">Azure AD StatusPage tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden StatusPage eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e8ac-125">**Galeriden StatusPage eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1e8ac-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e8ac-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e8ac-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1e8ac-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="1e8ac-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="1e8ac-133">Arama kutusuna **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-133">In the search box, type **StatusPage**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="1e8ac-135">Sonuçlar panelinde seçin **StatusPage**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e8ac-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1e8ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e8ac-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı StatusPage sınayın.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e8ac-139">Tekli çalışmaya oturum için Azure AD StatusPage karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="1e8ac-140">Diğer bir deyişle, bir Azure AD kullanıcısının StatusPage ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="1e8ac-141">StatusPage içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1e8ac-142">Yapılandırma ve Azure AD çoklu oturum açma StatusPage ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e8ac-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1e8ac-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e8ac-145">**[StatusPage test kullanıcısı oluşturma](#creating-a-statuspage-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı StatusPage sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e8ac-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e8ac-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e8ac-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1e8ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e8ac-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma StatusPage uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="1e8ac-150">**Azure AD çoklu oturum açma ile StatusPage yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1e8ac-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="1e8ac-151">Azure portalında üzerinde **StatusPage** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="1e8ac-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="1e8ac-155">Üzerinde **StatusPage etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="1e8ac-157">a.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-157">a.</span></span> <span data-ttu-id="1e8ac-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="1e8ac-159">b.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-159">b.</span></span> <span data-ttu-id="1e8ac-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="1e8ac-161">StatusPage destek ekibi ile iletişime geçin [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)çoklu oturum açma yapılandırmak için gerekli meta veri istemek için.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="1e8ac-162">a.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-162">a.</span></span> <span data-ttu-id="1e8ac-163">Meta verileri, veren değerini kopyalayın ve ardından yapıştırın **tanımlayıcısı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="1e8ac-164">b.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-164">b.</span></span> <span data-ttu-id="1e8ac-165">Meta veri yanıt URL'yi kopyalayın ve ardından yapıştırın **yanıt URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

4. <span data-ttu-id="1e8ac-166">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="1e8ac-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e8ac-170">Üzerinde **StatusPage yapılandırma** 'yi tıklatın **yapılandırma StatusPage** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1e8ac-171">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="1e8ac-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="1e8ac-173">Başka bir tarayıcı penceresinde StatusPage şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="1e8ac-174">Ana araç çubuğunda tıklatın **hesabı Yönet**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="1e8ac-176">Tıklatın **çoklu oturum açma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="1e8ac-178">SSO Kurulumu sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="1e8ac-181">a.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-181">a.</span></span> <span data-ttu-id="1e8ac-182">İçinde **SSO hedef URL** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1e8ac-183">b.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-183">b.</span></span> <span data-ttu-id="1e8ac-184">İndirilen sertifikanızı Not Defteri'nde açın, içeriği Kopyala ve ardından yapıştırın **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="1e8ac-185">c.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-185">c.</span></span> <span data-ttu-id="1e8ac-186">Tıklatın **yapılandırma kaydetme**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="1e8ac-187">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="1e8ac-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1e8ac-188">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1e8ac-189">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e8ac-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e8ac-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e8ac-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e8ac-191">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="1e8ac-193">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1e8ac-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e8ac-194">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e8ac-196">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e8ac-198">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e8ac-200">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1e8ac-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e8ac-202">a.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-202">a.</span></span> <span data-ttu-id="1e8ac-203">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e8ac-204">b.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-204">b.</span></span> <span data-ttu-id="1e8ac-205">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e8ac-206">c.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-206">c.</span></span> <span data-ttu-id="1e8ac-207">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1e8ac-208">d.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-208">d.</span></span> <span data-ttu-id="1e8ac-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="1e8ac-210">StatusPage test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e8ac-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="1e8ac-211">Bu bölümün amacı Britta Simon içinde StatusPage adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="1e8ac-212">Yalnızca zaman sağlama StatusPage destekler.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="1e8ac-213">İçinde zaten etkinleştirdiğiniz [yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="1e8ac-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="1e8ac-214">**İçinde StatusPage Britta Simon adlı bir kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1e8ac-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="1e8ac-215">StatusPage şirket sitenize yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-215">Sign-on to your StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="1e8ac-216">Üstteki menüde tıklatın **hesabı Yönet**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-216">In the menu on the top, click **Manage Account**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="1e8ac-218">Tıklatın **ekip üyelerinin** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-218">Click the **Team Members** tab.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="1e8ac-220">Tıklatın **Ekle ekip ÜYESİNE**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="1e8ac-222">Tür **e-posta adresi**, **ad**, ve **soyad** istediğiniz ilgili metin kutularına sağlamayı geçerli bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="1e8ac-224">Olarak **rol**, seçin **İstemci Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="1e8ac-225">Tıklatın **hesap oluştur**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1e8ac-226">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="1e8ac-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1e8ac-227">Bu bölümde, Britta StatusPage için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="1e8ac-229">**StatusPage için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1e8ac-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="1e8ac-230">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1e8ac-232">Uygulamalar listesinde **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-232">In the applications list, select **StatusPage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="1e8ac-234">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="1e8ac-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-236">Click **Add** button.</span></span> <span data-ttu-id="1e8ac-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="1e8ac-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1e8ac-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e8ac-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e8ac-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1e8ac-242">Testing single sign-on</span></span>

<span data-ttu-id="1e8ac-243">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1e8ac-244">Erişim paneli StatusPage parçasında tıklattığınızda, otomatik olarak StatusPage uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="1e8ac-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e8ac-245">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1e8ac-245">Additional resources</span></span>

* [<span data-ttu-id="1e8ac-246">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="1e8ac-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e8ac-247">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1e8ac-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

