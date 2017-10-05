---
title: "Öğretici: Azure Active Directory Tümleştirme ile Mixpanel | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Mixpanel arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3dd11b3477de1329c1c8e45a6dbf212b1635fd95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="1eb6a-103">Öğretici: Azure Active Directory Tümleştirme Mixpanel ile</span><span class="sxs-lookup"><span data-stu-id="1eb6a-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="1eb6a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Mixpanel tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1eb6a-105">Mixpanel Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1eb6a-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1eb6a-106">Mixpanel erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1eb6a-106">You can control in Azure AD who has access to Mixpanel</span></span>
- <span data-ttu-id="1eb6a-107">Otomatik olarak için Mixpanel (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1eb6a-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1eb6a-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="1eb6a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1eb6a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1eb6a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1eb6a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1eb6a-110">Prerequisites</span></span>

<span data-ttu-id="1eb6a-111">Azure AD tümleştirme Mixpanel ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="1eb6a-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

- <span data-ttu-id="1eb6a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1eb6a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1eb6a-113">Bir Mixpanel çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="1eb6a-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1eb6a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1eb6a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1eb6a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1eb6a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1eb6a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1eb6a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1eb6a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1eb6a-118">Scenario description</span></span>
<span data-ttu-id="1eb6a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1eb6a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1eb6a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1eb6a-121">Galeriden Mixpanel ekleme</span><span class="sxs-lookup"><span data-stu-id="1eb6a-121">Adding Mixpanel from the gallery</span></span>
2. <span data-ttu-id="1eb6a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1eb6a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-the-gallery"></a><span data-ttu-id="1eb6a-123">Galeriden Mixpanel ekleme</span><span class="sxs-lookup"><span data-stu-id="1eb6a-123">Adding Mixpanel from the gallery</span></span>
<span data-ttu-id="1eb6a-124">Azure AD Mixpanel tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Mixpanel eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1eb6a-125">**Galeriden Mixpanel eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1eb6a-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb6a-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1eb6a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1eb6a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="1eb6a-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="1eb6a-133">Arama kutusuna **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-133">In the search box, type **Mixpanel**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="1eb6a-135">Sonuçlar panelinde seçin **Mixpanel**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1eb6a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1eb6a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1eb6a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Mixpanel sınayın.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1eb6a-139">Tekli çalışmaya oturum için Azure AD Mixpanel karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span></span> <span data-ttu-id="1eb6a-140">Diğer bir deyişle, bir Azure AD kullanıcısının Mixpanel ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="1eb6a-141">Mixpanel içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1eb6a-142">Yapılandırma ve Azure AD çoklu oturum açma Mixpanel ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1eb6a-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1eb6a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1eb6a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1eb6a-145">**[Mixpanel test kullanıcısı oluşturma](#creating-a-mixpanel-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Mixpanel sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1eb6a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1eb6a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1eb6a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1eb6a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1eb6a-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Mixpanel uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="1eb6a-150">**Azure AD çoklu oturum açma ile Mixpanel yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1eb6a-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb6a-151">Azure portalında üzerinde **Mixpanel** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="1eb6a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="1eb6a-155">Üzerinde **Mixpanel etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1eb6a-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="1eb6a-157">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="1eb6a-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1eb6a-158">Lütfen adresindeki kayıt [https://mixpanel.com/register/](https://mixpanel.com/register/) oturum açma kimlik bilgileri ve iletişim kurmak için [Mixpanel destek ekibi](mailto:support@mixpanel.com) , kiracınızın SSO ayarlarını etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span></span> <span data-ttu-id="1eb6a-159">Ayrıca, üzerinde oturum URL değeri gerekirse Mixpanel destek ekibinden alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="1eb6a-160">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="1eb6a-162">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-162">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1eb6a-164">Üzerinde **Mixpanel yapılandırma** 'yi tıklatın **yapılandırma Mixpanel** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1eb6a-165">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="1eb6a-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="1eb6a-167">Farklı bir tarayıcı penceresinde Mixpanel uygulamanıza bir yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="1eb6a-168">Sayfanın en altındaki üzerinde biraz tıklatın **gear** sol alt köşesindeki simgesi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-168">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Mixpanel çoklu oturum açma](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="1eb6a-170">Tıklatın **erişim güvenlik** sekmesini ve ardından **Ayarları Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-170">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Mixpanel ayarları](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="1eb6a-172">Üzerinde **sertifikanızı değiştirme** iletişim sayfasında, tıklatın **dosya** indirilen sertifikanızı karşıya yükleyin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Mixpanel ayarları](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="1eb6a-174">Kimlik doğrulama URL'si metin kutusuna üzerinde **, kimlik doğrulaması URL'sini değiştirmek** iletişim sayfasında, değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** hangi Azure portalından kopyaladığınız ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Mixpanel ayarları](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="1eb6a-176">**Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="1eb6a-177">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="1eb6a-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1eb6a-178">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1eb6a-179">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1eb6a-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1eb6a-180">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1eb6a-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="1eb6a-181">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="1eb6a-183">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1eb6a-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb6a-184">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1eb6a-186">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1eb6a-188">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1eb6a-190">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1eb6a-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1eb6a-192">a.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-192">a.</span></span> <span data-ttu-id="1eb6a-193">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1eb6a-194">b.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-194">b.</span></span> <span data-ttu-id="1eb6a-195">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1eb6a-196">c.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-196">c.</span></span> <span data-ttu-id="1eb6a-197">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1eb6a-198">d.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-198">d.</span></span> <span data-ttu-id="1eb6a-199">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="1eb6a-200">Mixpanel test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1eb6a-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="1eb6a-201">Bu bölümün amacı Britta Simon içinde Mixpanel adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="1eb6a-202">Mixpanel şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-202">Sign on to your Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="1eb6a-203">Sayfanın üzerinde açmak için sol üst köşesinde küçük dişli düğmeyi tıklatın **ayarları** penceresi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>

3. <span data-ttu-id="1eb6a-204">Tıklatın **takım** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-204">Click the **Team** tab.</span></span>

4. <span data-ttu-id="1eb6a-205">İçinde **ekip üyesine** metin kutusuna, Azure Britta'nın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-205">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Mixpanel ayarları](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="1eb6a-207">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="1eb6a-208">Kullanıcı profili ayarlamak için bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-208">The user will get an email to set up the profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1eb6a-209">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="1eb6a-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1eb6a-210">Bu bölümde, Britta Mixpanel için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="1eb6a-212">**Mixpanel için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1eb6a-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="1eb6a-213">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1eb6a-215">Uygulamalar listesinde **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-215">In the applications list, select **Mixpanel**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="1eb6a-217">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="1eb6a-219">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-219">Click **Add** button.</span></span> <span data-ttu-id="1eb6a-220">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="1eb6a-222">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1eb6a-223">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1eb6a-224">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1eb6a-225">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1eb6a-225">Testing single sign-on</span></span>

<span data-ttu-id="1eb6a-226">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1eb6a-227">Erişim paneli Mixpanel parçasında tıklattığınızda, otomatik olarak Mixpanel uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="1eb6a-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>
<span data-ttu-id="1eb6a-228">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1eb6a-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1eb6a-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1eb6a-229">Additional resources</span></span>

* [<span data-ttu-id="1eb6a-230">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="1eb6a-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1eb6a-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1eb6a-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

