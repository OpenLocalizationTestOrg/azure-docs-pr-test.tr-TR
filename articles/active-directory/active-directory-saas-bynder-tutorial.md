---
title: "Öğretici: Azure Active Directory Tümleştirme ile Bynder | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Bynder arasında yapılandırmayı öğrenin."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="6a73d-103">Öğretici: Azure Active Directory Tümleştirme Bynder ile</span><span class="sxs-lookup"><span data-stu-id="6a73d-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="6a73d-104">Bu öğreticinin amacı Bynder Azure Active Directory (Azure AD) ile tümleştirme Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="6a73d-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a73d-105">Bynder Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6a73d-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="6a73d-106">Bynder erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6a73d-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="6a73d-107">Otomatik olarak Bynder çoklu oturum açma (SSO) ile Azure AD hesaplarına için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6a73d-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="6a73d-108">Hesaplarınızı bir merkezi konumda - Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="6a73d-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="6a73d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a73d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a73d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6a73d-110">Prerequisites</span></span>
<span data-ttu-id="6a73d-111">Azure AD tümleştirme Bynder ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a73d-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="6a73d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6a73d-112">An Azure AD subscription</span></span>
* <span data-ttu-id="6a73d-113">Abonelik bir Bynder çoklu oturum açma (SSO) etkin</span><span class="sxs-lookup"><span data-stu-id="6a73d-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="6a73d-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6a73d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="6a73d-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a73d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="6a73d-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a73d-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="6a73d-117">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a73d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a73d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6a73d-118">Scenario description</span></span>
<span data-ttu-id="6a73d-119">Bu öğreticinin amacı, Microsoft Azure AD SSO bir test ortamında test etmenizi hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="6a73d-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="6a73d-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6a73d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a73d-121">Galeriden Bynder ekleme</span><span class="sxs-lookup"><span data-stu-id="6a73d-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="6a73d-122">Yapılandırma ve Microsoft Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="6a73d-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="6a73d-123">Galeriden Bynder Ekle</span><span class="sxs-lookup"><span data-stu-id="6a73d-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="6a73d-124">Azure AD Bynder tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Bynder eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a73d-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a73d-125">**Galeriden Bynder eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a73d-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a73d-126">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="6a73d-128">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="6a73d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6a73d-129">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="6a73d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Uygulamalar][2]
4. <span data-ttu-id="6a73d-131">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="6a73d-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Uygulamalar][3]
5. <span data-ttu-id="6a73d-133">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Uygulamalar][4]
6. <span data-ttu-id="6a73d-135">Arama kutusuna **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-135">In the search box, type **Bynder**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="6a73d-137">Sonuçlar panelinde seçin **Bynder**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="6a73d-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![Uygulama galerisinde seçme](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="6a73d-139">Yapılandırma ve Microsoft Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="6a73d-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="6a73d-140">Bu bölümün amacı, size nasıl yapılandırılacağı ve Microsoft Azure AD "Britta Simon" adlı bir test kullanıcı tabanlı Bynder SSO'su test göstermektir.</span><span class="sxs-lookup"><span data-stu-id="6a73d-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a73d-141">Çalışmak SSO için Azure AD Bynder Azure AD'de bir kullanıcıya karşılık gelen kullanıcı ne olduğunu bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a73d-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="6a73d-142">Diğer bir deyişle, bir Azure AD kullanıcısının Bynder ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a73d-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="6a73d-143">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Bynder içinde.</span><span class="sxs-lookup"><span data-stu-id="6a73d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="6a73d-144">Yapılandırmak ve Microsoft Azure AD Bynder SSO'su sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a73d-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a73d-145">**[Microsoft Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6a73d-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a73d-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Microsoft Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="6a73d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="6a73d-147">**[Bynder test kullanıcısı oluşturma](#creating-a-bynder-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı Bynder sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="6a73d-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6a73d-148">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Britta Microsoft Azure AD çoklu oturum açma kullanmak Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6a73d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="6a73d-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6a73d-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="6a73d-150">Microsoft Azure AD SSO yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6a73d-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="6a73d-151">Bu bölümde, Microsoft Azure AD SSO Klasik portalda etkinleştirin ve SSO Bynder uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6a73d-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="6a73d-152">**Microsoft Azure AD SSO ile Bynder yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a73d-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="6a73d-153">Klasik Portalı'ndaki üzerinde **Bynder** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırmak** açmak için **yapılandırma çoklu oturum açma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6a73d-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. <span data-ttu-id="6a73d-155">Üzerinde **Bynder için oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="6a73d-157">Üzerinde **uygulama ayarlarını yapılandır** iletişim sayfa, uygulamada yapılandırmak istiyorsanız **IDP başlatılan modu**, aşağıdaki adımları gerçekleştirin ve tıklayın **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="6a73d-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="6a73d-159">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="6a73d-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="6a73d-160">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a73d-160">Click **Next**.</span></span>
4. <span data-ttu-id="6a73d-161">Uygulamada yapılandırmak istiyorsanız **SP tarafından başlatılan modu** üzerinde **uygulama ayarlarını yapılandır** iletişim sayfa sonra tıklatıldığında **"Göster Gelişmiş ayarları (isteğe bağlı)"** ve enter **oturum üzerinde URL'si** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="6a73d-163">İçinde **oturum üzerinde URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="6a73d-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="6a73d-164">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a73d-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="6a73d-165">Bu öğretici oturum üzerinde URL'si için yalnızca bir placeholfer değerdir.</span><span class="sxs-lookup"><span data-stu-id="6a73d-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="6a73d-166">Ortamınız için gerçek vlaue almak için Bynder başvurun.</span><span class="sxs-lookup"><span data-stu-id="6a73d-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="6a73d-167">Üzerinde **çoklu oturum açma sırasında Bynder yapılandırma** sayfasında, aşağıdaki adımları gerçekleştirin ve tıklayın **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="6a73d-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="6a73d-169">Tıklatın **karşıdan meta veri**ve ardından dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6a73d-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="6a73d-170">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a73d-170">Click **Next**.</span></span>
6. <span data-ttu-id="6a73d-171">Uygulamanız için yapılandırılmış SSO almak için Bynder destek ekibinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="6a73d-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="6a73d-172">İndirilen meta veri dosyası ekleme ve bunların tarafında SSO'yu ayarlamak için Bynder ekibi ile paylaşın.</span><span class="sxs-lookup"><span data-stu-id="6a73d-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="6a73d-173">Klasik Portalı'ndaki tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][10]
8. <span data-ttu-id="6a73d-175">Üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD çoklu oturum açma][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6a73d-177">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a73d-177">Create an Azure AD test user</span></span>
<span data-ttu-id="6a73d-178">Bu bölümün amacı, Britta Simon adlı Klasik portalda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="6a73d-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="6a73d-180">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a73d-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a73d-181">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="6a73d-183">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="6a73d-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6a73d-184">Üstteki menüde kullanıcıların listesini görüntülemek için tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="6a73d-186">Açmak için **Kullanıcı Ekle** iletişim kutusunda, araç çubuğunda alt tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="6a73d-188">Üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a73d-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="6a73d-190">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="6a73d-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="6a73d-191">Kullanıcı adı **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="6a73d-192">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a73d-192">Click **Next**.</span></span>
6. <span data-ttu-id="6a73d-193">Üzerinde **kullanıcı profili** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a73d-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="6a73d-195">İçinde **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="6a73d-196">İçinde **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="6a73d-197">İçinde **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="6a73d-198">İçinde **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="6a73d-199">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a73d-199">Click **Next**.</span></span>
7. <span data-ttu-id="6a73d-200">Üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="6a73d-202">Üzerinde **Get geçici parola** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a73d-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="6a73d-204">Değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="6a73d-205">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a73d-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="6a73d-206">Bynder test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a73d-206">Create a Bynder test user</span></span>
<span data-ttu-id="6a73d-207">Bu bölümün amacı Britta Simon içinde Bynder adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="6a73d-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="6a73d-208">Bynder yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="6a73d-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="6a73d-209">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="6a73d-209">There is no action item for you in this section.</span></span> <span data-ttu-id="6a73d-210">Yeni bir kullanıcı henüz yoksa Bynder erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6a73d-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="6a73d-211">Bir kullanıcı el ile oluşturmanız gerekiyorsa, Bynder Destek ekibine başvurun gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a73d-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6a73d-212">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="6a73d-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="6a73d-213">Bu bölümün amacı Britta Bynder için kendi erişim vererek Azure SSO kullanılacak Simon için etkinleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="6a73d-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![Kullanıcı atama][200]

<span data-ttu-id="6a73d-215">**Bynder için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a73d-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="6a73d-216">Klasik portalı üzerinde dizin görünümünde uygulamaları görünümü açmak için tıklatın **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="6a73d-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Kullanıcı atama][201]
2. <span data-ttu-id="6a73d-218">Uygulamalar listesinde **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-218">In the applications list, select **Bynder**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="6a73d-220">Üstteki menüde tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-220">In the menu on the top, click **Users**.</span></span>
   
    ![Kullanıcı atama][203]
4. <span data-ttu-id="6a73d-222">Kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="6a73d-223">Araç çubuğunda alt tıklatın **atamak**.</span><span class="sxs-lookup"><span data-stu-id="6a73d-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="6a73d-225">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="6a73d-225">Test single sign-on</span></span>
<span data-ttu-id="6a73d-226">Bu bölümün amacı erişim paneli kullanılarak Microsoft Azure AD SSO yapılandırmanızı test sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="6a73d-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6a73d-227">Erişim paneli Bynder parçasında tıklattığınızda, otomatik olarak Bynder uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="6a73d-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a73d-228">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6a73d-228">Additional resources</span></span>
* [<span data-ttu-id="6a73d-229">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="6a73d-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a73d-230">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6a73d-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
