---
title: "Öğretici: Azure Active Directory Tümleştirme Splunk Kurumsal ve Splunk bulut ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Splunk Enterprise ve Splunk bulut arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="8c92d-103">Öğretici: Azure Active Directory Tümleştirme Splunk Kurumsal ve Splunk bulut ile</span><span class="sxs-lookup"><span data-stu-id="8c92d-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="8c92d-104">Bu öğreticide, bilgi nasıl toointegrate Splunk Kurumsal ve Splunk bulut Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c92d-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c92d-105">Splunk Kurumsal ve Splunk bulut Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8c92d-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8c92d-106">TooSplunk Kurumsal ve Splunk bulut erişimi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8c92d-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="8c92d-107">Azure AD hesaplarına, kullanıcıların tooautomatically get açan tooSplunk Kurumsal ve Splunk bulut çoklu oturum açma (SSO) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="8c92d-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="8c92d-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="8c92d-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="8c92d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c92d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c92d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8c92d-110">Prerequisites</span></span>

<span data-ttu-id="8c92d-111">Azure AD ile tümleştirme Splunk Enterprise ve Splunk bulut tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8c92d-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="8c92d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8c92d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c92d-113">Abonelik Splunk Enterprise veya Splunk bulut SSO etkin</span><span class="sxs-lookup"><span data-stu-id="8c92d-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="8c92d-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8c92d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="8c92d-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="8c92d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c92d-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c92d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8c92d-117">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c92d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="8c92d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8c92d-118">Scenario description</span></span>
<span data-ttu-id="8c92d-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8c92d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="8c92d-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8c92d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c92d-121">Splunk Kurumsal ve Splunk bulut hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="8c92d-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="8c92d-122">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="8c92d-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="8c92d-123">Splunk Kurumsal ve Splunk bulut hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="8c92d-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="8c92d-124">SaaS uygulamaları listesinden hello galeri tooyour Splunk bulut yönetilen ve Azure AD'ye tooconfigure hello tümleştirme Splunk Enterprise ve Splunk bulut tooadd Splunk Kurumsal gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c92d-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8c92d-125">**tooadd Splunk Kurumsal ve Splunk bulut hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8c92d-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c92d-126">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="8c92d-128">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="8c92d-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="8c92d-129">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="8c92d-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Uygulamalar][2]

4. <span data-ttu-id="8c92d-131">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="8c92d-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Uygulamalar][3]

5. <span data-ttu-id="8c92d-133">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Uygulamalar][4]

6. <span data-ttu-id="8c92d-135">Merhaba arama kutusuna yazın **Splunk Enterprise veya Splunk bulut**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="8c92d-137">Merhaba sonuçlar bölmesinde seçin **Splunk Kurumsal ve Splunk bulut**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8c92d-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8c92d-139">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8c92d-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8c92d-140">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Splunk kuruluş ile test etme ve "Britta Simon" adlı bir test kullanıcı Splunk bulut tabanlı.</span><span class="sxs-lookup"><span data-stu-id="8c92d-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8c92d-141">Tek toowork'ın oturum açma hangi hello karşılık gelen Splunk Kurumsal ve Splunk bulut tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c92d-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="8c92d-142">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Splunk Kurumsal ve Splunk bulut arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c92d-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="8c92d-143">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Splunk Kurumsal ve Splunk bulut.</span><span class="sxs-lookup"><span data-stu-id="8c92d-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="8c92d-144">tooconfigure ve Splunk Kurumsal ve Splunk bulut ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8c92d-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8c92d-145">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="8c92d-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8c92d-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="8c92d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c92d-147">**[Splunk Kurumsal ve Splunk bulut test kullanıcısı oluşturma](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave karşılık gelen Britta Simon Splunk kuruluştaki ve her bağlantılı toohello Azure AD gösterimidir Splunk bulut.</span><span class="sxs-lookup"><span data-stu-id="8c92d-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8c92d-148">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8c92d-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c92d-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="8c92d-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8c92d-150">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8c92d-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8c92d-151">Bu bölümde, Azure AD SSO hello Klasik portalında etkinleştirin ve SSO Splunk Kurumsal ve Splunk bulut uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8c92d-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="8c92d-152">**Azure AD çoklu oturum açma tooconfigure Splunk Kurumsal ve Splunk bulut ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8c92d-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c92d-153">Hello üzerinde hello Klasik Portalı'nda **Splunk Kurumsal ve Splunk bulut** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8c92d-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Çoklu oturum açmayı yapılandırın][6] 

2. <span data-ttu-id="8c92d-155">Merhaba üzerinde **nasıl istiyorsunuz tooSplunk Kurumsal üzerinde kullanıcılar toosign ve Splunk bulut** sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="8c92d-157">Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8c92d-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="8c92d-159">Merhaba, **oturum üzerinde URL'si** metin kutusuna, kullanıcıların toosign üzerinde tooyour Splunk Enterprise ve desen aşağıdaki hello kullanarak Splunk bulut uygulaması tarafından kullanılan türü hello URL'si:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="8c92d-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="8c92d-160">Merhaba, **tanımlayıcısı** metin kutusuna, Splunk sunucunuzun hello URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="8c92d-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="8c92d-161">Merhaba, **yanıt URL'si** metin kutusuna, türü hello URL deseni takip hello ile:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="8c92d-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="8c92d-162">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c92d-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="8c92d-163">Merhaba üzerinde **çoklu oturum açma Splunk Enterprise ve Splunk bulut yapılandırma** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8c92d-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="8c92d-165">Tıklatın **karşıdan meta veri**ve ardından hello dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8c92d-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="8c92d-166">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c92d-166">Click **Next**.</span></span>

5. <span data-ttu-id="8c92d-167">tooget uygulamanız için yapılandırılmış SSO Splunk Enterprise ve Splunk bulut Destek ekibine başvurun ve ile Merhaba aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="8c92d-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="8c92d-168">indirilen hello **federaton meta verileri**</span><span class="sxs-lookup"><span data-stu-id="8c92d-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="8c92d-169">Merhaba Klasik portalında hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD çoklu oturum açma][10]

7. <span data-ttu-id="8c92d-171">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD çoklu oturum açma][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8c92d-173">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c92d-173">Create an Azure AD test user</span></span>
<span data-ttu-id="8c92d-174">Bu bölümde, bir test kullanıcısı Britta Simon adlı hello Klasik portalda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c92d-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="8c92d-176">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8c92d-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c92d-177">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="8c92d-179">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="8c92d-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="8c92d-180">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c92d-182">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="8c92d-184">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8c92d-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="8c92d-186">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="8c92d-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="8c92d-187">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="8c92d-188">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c92d-188">Click **Next**.</span></span>

6.  <span data-ttu-id="8c92d-189">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8c92d-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="8c92d-191">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="8c92d-192">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="8c92d-193">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="8c92d-194">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="8c92d-195">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c92d-195">Click **Next**.</span></span>

7. <span data-ttu-id="8c92d-196">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="8c92d-198">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8c92d-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="8c92d-200">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="8c92d-201">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c92d-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="8c92d-202">Splunk Enterprise ve Splunk bulut test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c92d-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="8c92d-203">Bu bölümde, Britta Simon Splunk kuruluştaki ve Splunk bulut adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c92d-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="8c92d-204">Lütfen destek ekibi tooadd hello kullanıcılar hello Splunk Enterprise ve Splunk bulut platformu Splunk Enterprise ve Splunk bulut çalışın.</span><span class="sxs-lookup"><span data-stu-id="8c92d-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8c92d-205">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="8c92d-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8c92d-206">Bu bölümde, Britta Simon toouse Azure kendi erişim tooSplunk Kurumsal ve Splunk bulut verme SSOy etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8c92d-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8c92d-208">**tooassign Britta Simon tooSplunk Enterprise ve Splunk bulut hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8c92d-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c92d-209">Merhaba Klasik portalında hello dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="8c92d-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8c92d-211">Merhaba uygulamalar listesinde **Splunk Kurumsal ve Splunk bulut**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="8c92d-213">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-213">In hello menu on hello top, click **Users**.</span></span>

    ![Kullanıcı atama][203]

4. <span data-ttu-id="8c92d-215">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="8c92d-216">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="8c92d-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Kullanıcı atama][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="8c92d-218">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="8c92d-218">Test single sign-on</span></span>

<span data-ttu-id="8c92d-219">Bu bölümde, Azure AD erişim paneli hello kullanarak SSOonfiguration test edin.</span><span class="sxs-lookup"><span data-stu-id="8c92d-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="8c92d-220">Merhaba Splunk Enterprise ve erişim paneli hello Splunk bulut parçasında tıkladığınızda, otomatik olarak oturum açma Splunk Kurumsal ve Splunk bulut uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c92d-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8c92d-221">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8c92d-221">Additional resources</span></span>

* [<span data-ttu-id="8c92d-222">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8c92d-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c92d-223">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8c92d-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
