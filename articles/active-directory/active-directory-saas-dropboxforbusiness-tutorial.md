---
title: "Öğretici: İş için Dropbox Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve iş için Dropbox arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a56a5af171eaca259db29f25fee4331a77313420
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="c7a1b-103">Öğretici: İş için Dropbox Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="c7a1b-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="c7a1b-104">Bu öğreticide, Dropbox iş için Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7a1b-105">Dropbox iş için Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c7a1b-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7a1b-106">İş Dropbox erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c7a1b-106">You can control in Azure AD who has access to Dropbox for Business</span></span>
- <span data-ttu-id="c7a1b-107">Otomatik olarak iş (çoklu oturum açma) için Dropbox için Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c7a1b-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7a1b-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c7a1b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7a1b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7a1b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7a1b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c7a1b-110">Prerequisites</span></span>

<span data-ttu-id="c7a1b-111">İş için Dropbox ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="c7a1b-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="c7a1b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c7a1b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7a1b-113">Bir Dropbox iş çoklu oturum açma için abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c7a1b-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7a1b-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7a1b-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c7a1b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7a1b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7a1b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7a1b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7a1b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c7a1b-118">Scenario description</span></span>
<span data-ttu-id="c7a1b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7a1b-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c7a1b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7a1b-121">İş için Dropbox Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="c7a1b-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="c7a1b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c7a1b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="c7a1b-123">İş için Dropbox Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="c7a1b-123">Adding Dropbox for Business from the gallery</span></span>
<span data-ttu-id="c7a1b-124">Azure AD içinde iş için Dropbox tümleştirmesini yapılandırmak için iş için Dropbox Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7a1b-125">**İş için Dropbox Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c7a1b-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7a1b-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7a1b-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7a1b-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c7a1b-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-131">Click **New application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c7a1b-133">Arama kutusuna **iş için Dropbox**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-133">In the search box, type **Dropbox for Business**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="c7a1b-135">Sonuçlar panelinde seçin **iş için Dropbox**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-135">In the results panel, select **Dropbox for Business**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7a1b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c7a1b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7a1b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı iş için Dropbox ile test etme</span><span class="sxs-lookup"><span data-stu-id="c7a1b-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7a1b-139">Tekli çalışmaya oturum için Azure AD iş için Dropbox karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="c7a1b-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve kurumsal Dropbox ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-140">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="c7a1b-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** iş için Dropbox içinde.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="c7a1b-142">Yapılandırma ve Azure AD çoklu oturum açma iş için Dropbox ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c7a1b-142">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7a1b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7a1b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7a1b-145">**[Bir Dropbox iş test kullanıcısı için oluşturma](#creating-a-dropbox-for-business-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı iş için Dropbox sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7a1b-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7a1b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7a1b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c7a1b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7a1b-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma, Dropbox iş uygulaması için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="c7a1b-150">**İş için Dropbox ile Azure AD çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c7a1b-150">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="c7a1b-151">Azure portalında üzerinde **Dropbox iş için** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-151">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c7a1b-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="c7a1b-155">Üzerinde **iş etki alanı ve URL'ler için Dropbox** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c7a1b-155">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="c7a1b-156">a.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-156">a.</span></span> <span data-ttu-id="c7a1b-157">İş Kiracı için Dropbox oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-157">Sign on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="c7a1b-158">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="c7a1b-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="c7a1b-159">b.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-159">b.</span></span> <span data-ttu-id="c7a1b-160">Sol taraftaki gezinti bölmesinde tıklayın **Yönetici Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-160">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="c7a1b-161">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="c7a1b-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="c7a1b-162">c.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-162">c.</span></span> <span data-ttu-id="c7a1b-163">Üzerinde **Yönetici Konsolu**, tıklatın **kimlik doğrulaması** sol gezinti bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-163">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="c7a1b-164">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="c7a1b-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="c7a1b-165">d.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-165">d.</span></span> <span data-ttu-id="c7a1b-166">İçinde **çoklu oturum açma** bölümünde, select **çoklu oturum açmayı etkinleştir**ve ardından **daha fazla** bu bölümü genişletin.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-166">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="c7a1b-167">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="c7a1b-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="c7a1b-168">e.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-168">e.</span></span> <span data-ttu-id="c7a1b-169">URL'yi yanına kopyalayın **kullanıcılar uygulamasında oturum açabilir, e-posta adreslerini girerek veya doğrudan gidebilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-169">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="c7a1b-171">f.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-171">f.</span></span> <span data-ttu-id="c7a1b-172">Azure portalındaki içinde **oturum açma URL'si** metin kutusuna, URL yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-172">On the Azure portal, in the **Sign-on URL** textbox, paste the URL.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="c7a1b-174">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="c7a1b-174">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7a1b-175">Bu değer gerçek değeri değil.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-175">This value is not real value.</span></span> <span data-ttu-id="c7a1b-176">Kendi tek oturum açma bölümünden alma gerçek oturum açma URL'si ile değeri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-176">Update the value with the actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="c7a1b-177">Kişi [iş istemci destek ekibi için Dropbox](https://www.dropbox.com/business/contact) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="c7a1b-178">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="c7a1b-180">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-180">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7a1b-182">Üzerinde **iş yapılandırması için Dropbox** 'yi tıklatın **iş için yapılandırma Dropbox** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-182">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c7a1b-183">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c7a1b-183">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="c7a1b-185">Çoklu oturum açma yapılandırmak için **iş için Dropbox** tarafı, iş Kiracı için açılan kutu içinde gidin **çoklu oturum açma** bölümünü **kimlik doğrulama** sayfasında, gerçekleştirin Aşağıdaki adımlar:</span><span class="sxs-lookup"><span data-stu-id="c7a1b-185">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="c7a1b-186">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="c7a1b-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="c7a1b-187">a.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-187">a.</span></span> <span data-ttu-id="c7a1b-188">Tıklatın **gerekli**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-188">Click **Required**.</span></span>
   
    <span data-ttu-id="c7a1b-189">b.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-189">b.</span></span> <span data-ttu-id="c7a1b-190">Azure portalında üzerinde **yapılandırma oturum açma** penceresinde, kopya **SAML çoklu oturum açma hizmet URL'si** değer ve ardından yapıştırın **oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-190">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="c7a1b-191">c.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-191">c.</span></span> <span data-ttu-id="c7a1b-192">Tıklatın **Sertifika Seç**ve ardından göz atın, **Base64 ile kodlanmış sertifika dosyası**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-192">Click **Choose certificate**, and then browse to your **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="c7a1b-193">d.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-193">d.</span></span> <span data-ttu-id="c7a1b-194">Tıklatın **değişiklikleri kaydetmek** , DropBox iş Kiracı için üzerindeki yapılandırmayı tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-194">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="c7a1b-195">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c7a1b-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7a1b-196">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7a1b-197">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7a1b-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7a1b-198">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7a1b-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7a1b-199">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c7a1b-201">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c7a1b-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7a1b-202">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="c7a1b-204">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7a1b-206">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-206">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7a1b-208">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c7a1b-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7a1b-210">a.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-210">a.</span></span> <span data-ttu-id="c7a1b-211">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7a1b-212">b.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-212">b.</span></span> <span data-ttu-id="c7a1b-213">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7a1b-214">c.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-214">c.</span></span> <span data-ttu-id="c7a1b-215">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7a1b-216">d.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-216">d.</span></span> <span data-ttu-id="c7a1b-217">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="c7a1b-218">Bir Dropbox iş test kullanıcısı için oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7a1b-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="c7a1b-219">Bu bölümde, iş için Dropbox Britta Simon adlı bir kullanıcı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="c7a1b-220">İş için Dropbox tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="c7a1b-221">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-221">There is no action item for you in this section.</span></span> <span data-ttu-id="c7a1b-222">İş için Dropbox'ın bir kullanıcı zaten mevcut değilse yeni bir iş için Dropbox erişmeyi denediğinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="c7a1b-223">Bir kullanıcı el ile oluşturmanız gerekirse başvurun [iş istemci destek ekibi için açılan kutu](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="c7a1b-223">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c7a1b-224">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c7a1b-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c7a1b-225">Bu bölümde, iş için Dropbox için erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c7a1b-227">**İş için Dropbox Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c7a1b-227">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="c7a1b-228">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c7a1b-230">Uygulamalar listesinde **iş için Dropbox**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-230">In the applications list, select **Dropbox for Business**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="c7a1b-232">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c7a1b-234">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-234">Click **Add** button.</span></span> <span data-ttu-id="c7a1b-235">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c7a1b-237">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7a1b-238">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7a1b-239">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7a1b-240">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c7a1b-240">Testing single sign-on</span></span>

<span data-ttu-id="c7a1b-241">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c7a1b-242">Erişim paneli iş parçasında Dropbox'ı tıklattığınızda, Dropbox oturum açma sayfasında iş uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7a1b-242">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7a1b-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c7a1b-243">Additional resources</span></span>

* [<span data-ttu-id="c7a1b-244">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="c7a1b-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7a1b-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c7a1b-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c7a1b-246">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="c7a1b-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

