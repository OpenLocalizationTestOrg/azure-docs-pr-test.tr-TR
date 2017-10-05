---
title: "Öğretici: Azure Active Directory Tümleştirme Wizergos üretkenlik ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Wizergos üretkenlik arasında yapılandırmayı öğrenin."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 73b3bc05aeb337c12acb7e47c0dbebe6d0196530
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="02c6f-103">Öğretici: Azure Active Directory Tümleştirme ile Wizergos üretkenlik</span><span class="sxs-lookup"><span data-stu-id="02c6f-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="02c6f-104">Bu öğreticinin amacı Wizergos üretkenlik Azure Active Directory (Azure AD) ile tümleştirme Göster sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="02c6f-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02c6f-105">Wizergos üretkenlik Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="02c6f-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="02c6f-106">Wizergos üretkenlik erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="02c6f-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="02c6f-107">Otomatik olarak Wizergos üretkenlik çoklu oturum açma (SSO) ile Azure AD hesaplarına için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="02c6f-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="02c6f-108">Hesaplarınızı bir merkezi konumda - Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="02c6f-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="02c6f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02c6f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02c6f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="02c6f-110">Prerequisites</span></span>
<span data-ttu-id="02c6f-111">Azure AD tümleştirme Wizergos üretkenlik ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="02c6f-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="02c6f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="02c6f-112">An Azure AD subscription</span></span>
* <span data-ttu-id="02c6f-113">Abonelik Wizergos üretkenlik yazılım SSO etkin</span><span class="sxs-lookup"><span data-stu-id="02c6f-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="02c6f-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="02c6f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="02c6f-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="02c6f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="02c6f-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="02c6f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="02c6f-117">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02c6f-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02c6f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="02c6f-118">Scenario description</span></span>
<span data-ttu-id="02c6f-119">Bu öğreticinin amacı, Azure AD SSO bir test ortamında test etmenizi hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="02c6f-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="02c6f-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="02c6f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02c6f-121">Galeriden Wizergos üretkenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="02c6f-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="02c6f-122">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="02c6f-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="02c6f-123">Galeriden Wizergos üretkenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="02c6f-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="02c6f-124">Azure AD Wizergos üretkenlik tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Wizergos üretkenlik eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="02c6f-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02c6f-125">**Galeriden Wizergos üretkenlik eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="02c6f-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02c6f-126">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="02c6f-128">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="02c6f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="02c6f-129">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="02c6f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Uygulamalar][2]
4. <span data-ttu-id="02c6f-131">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="02c6f-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Uygulamalar][3]
5. <span data-ttu-id="02c6f-133">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Uygulamalar][4]
6. <span data-ttu-id="02c6f-135">Arama kutusuna **Wizergos üretkenlik**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="02c6f-137">Sonuçlar panelinde seçin **Wizergos üretkenlik**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="02c6f-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![Uygulama galerisinde seçme](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="02c6f-139">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="02c6f-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="02c6f-140">Bu bölümün amacı, size nasıl yapılandırılacağı ve Azure AD "Britta Simon" adlı bir test kullanıcı tabanlı Wizergos üretkenlik SSO'su test göstermektir.</span><span class="sxs-lookup"><span data-stu-id="02c6f-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02c6f-141">Çalışmak SSO için Azure AD Wizergos üretkenlik Azure AD'de bir kullanıcıya karşılık gelen kullanıcı ne olduğunu bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="02c6f-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="02c6f-142">Diğer bir deyişle, bir Azure AD kullanıcısının Wizergos üretkenlik ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="02c6f-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="02c6f-143">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Wizergos üretkenlik yazılım.</span><span class="sxs-lookup"><span data-stu-id="02c6f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="02c6f-144">Yapılandırma ve Azure AD çoklu oturum açma BynWizergos üretkenlik Softwareder ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="02c6f-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02c6f-145">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="02c6f-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02c6f-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="02c6f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02c6f-147">**[Wizergos üretkenlik test kullanıcısı oluşturma](#creating-a-wizergos-productivity-software-test-user)**  - Britta Simon, karşılık gelen Wizergos Azure AD gösterimini her için bağlantılı üretkenlik sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="02c6f-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="02c6f-148">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="02c6f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02c6f-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="02c6f-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="02c6f-150">Azure AD SSO yapılandırma</span><span class="sxs-lookup"><span data-stu-id="02c6f-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="02c6f-151">Bu bölümde, Azure AD çoklu oturum açma Klasik portalında etkinleştirin ve çoklu oturum açma Wizergos üretkenlik uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="02c6f-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="02c6f-152">**Azure AD çoklu oturum açma Wizergos üretkenlik ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="02c6f-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="02c6f-153">Klasik Portalı'ndaki üzerinde **Wizergos üretkenlik** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma yapılandırmak** açmak için **yapılandırma çoklu oturum açma**  iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="02c6f-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. <span data-ttu-id="02c6f-155">Üzerinde **Wizergos üretkenlik oturum açmasını nasıl istiyorsunuz** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="02c6f-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="02c6f-157">Üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, tıklatın **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="02c6f-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="02c6f-159">Üzerinde **çoklu oturum açma sırasında Wizergos üretkenlik yapılandırma** sayfasında, **indirme sertifika**ve ardından dosyayı bilgisayarınıza kaydedin:</span><span class="sxs-lookup"><span data-stu-id="02c6f-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="02c6f-161">Farklı web tarayıcısı penceresinde Wizergos üretkenlik kiracınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="02c6f-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="02c6f-162">Hamburger menüsünden seçin **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="02c6f-164">Sol taraftaki menüsünde Yönetim sayfasında seçin **kimlik doğrulaması** ve tıklayın **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="02c6f-166">Aşağıdaki adımları gerçekleştirin **kimlik doğrulaması** bölümü.</span><span class="sxs-lookup"><span data-stu-id="02c6f-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="02c6f-168">Tıklatın **karşıya** Azure AD'den indirilen sertifikayı karşıya yüklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="02c6f-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="02c6f-169">İçinde **veren URL'si** textbox değeri put **veren URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="02c6f-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="02c6f-170">İçinde **çoklu oturum açma URL'si** textbox değeri put **çoklu oturum açma hizmet URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="02c6f-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="02c6f-171">İçinde **tek Sign-Out URL** textbox değeri put **tek Sign-out hizmeti URL'si** Azure AD Uygulama Yapılandırma Sihirbazı'ndan.</span><span class="sxs-lookup"><span data-stu-id="02c6f-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="02c6f-172">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="02c6f-172">Click **Save** button.</span></span>
9. <span data-ttu-id="02c6f-173">Klasik Portalı'ndaki tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][10]
10. <span data-ttu-id="02c6f-175">Üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD çoklu oturum açma][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="02c6f-177">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="02c6f-177">Create an Azure AD test user</span></span>
<span data-ttu-id="02c6f-178">Bu bölümün amacı, Britta Simon adlı Klasik portalda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="02c6f-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="02c6f-180">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="02c6f-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02c6f-181">İçinde **Klasik Azure portalı**, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="02c6f-183">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="02c6f-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="02c6f-184">Üstteki menüde kullanıcıların listesini görüntülemek için tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="02c6f-186">Açmak için **Kullanıcı Ekle** iletişim kutusunda, araç çubuğunda alt tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="02c6f-188">Üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="02c6f-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="02c6f-190">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="02c6f-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="02c6f-191">Kullanıcı adı **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="02c6f-192">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02c6f-192">Click **Next**.</span></span>
6. <span data-ttu-id="02c6f-193">Üzerinde **kullanıcı profili** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="02c6f-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="02c6f-195">İçinde **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="02c6f-196">İçinde **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="02c6f-197">İçinde **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="02c6f-198">İçinde **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="02c6f-199">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02c6f-199">Click **Next**.</span></span>
7. <span data-ttu-id="02c6f-200">Üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="02c6f-202">Üzerinde **Get geçici parola** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="02c6f-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="02c6f-204">Değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="02c6f-205">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02c6f-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="02c6f-206">Wizergos üretkenlik test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="02c6f-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="02c6f-207">Bu bölümde, Britta Simon Wizergos üretkenlik adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="02c6f-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="02c6f-208">Lütfen Wizergos üretkenlik destek ekibi ile çalışmak [ support@wizergos.com ](emailTo:support@wizergos.com) Wizergos üretkenlik platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="02c6f-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="02c6f-209">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="02c6f-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="02c6f-210">Bu bölümün amacı Britta Wizergos üretkenlik her erişim vererek Azure SSO kullanılacak Simon için etkinleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="02c6f-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![Kullanıcı atama][200]

<span data-ttu-id="02c6f-212">**Britta Simon Wizergos üretkenlik atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="02c6f-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="02c6f-213">Klasik portalı üzerinde dizin görünümünde uygulamaları görünümü açmak için tıklatın **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="02c6f-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Kullanıcı atama][201]
2. <span data-ttu-id="02c6f-215">Uygulamalar listesinde **Wizergos üretkenlik**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="02c6f-217">Üstteki menüde tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-217">In the menu on the top, click **Users**.</span></span>
   
    ![Kullanıcı atama][203]
4. <span data-ttu-id="02c6f-219">Kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="02c6f-220">Araç çubuğunda alt tıklatın **atamak**.</span><span class="sxs-lookup"><span data-stu-id="02c6f-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="02c6f-222">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="02c6f-222">Test single sign-on</span></span>
<span data-ttu-id="02c6f-223">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="02c6f-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="02c6f-224">Erişim paneli Wizergos üretkenlik parçasında tıklattığınızda, otomatik olarak Wizergos üretkenlik uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="02c6f-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="02c6f-225">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="02c6f-225">Additional resources</span></span>
* [<span data-ttu-id="02c6f-226">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="02c6f-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02c6f-227">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="02c6f-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
