---
title: "Öğretici: Azure Active Directory Tümleştirme ile IdeaScale | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile IdeaScale arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 88099e942319f16dd721da83e4e69b8fcb836c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="48fc8-103">Öğretici: Azure Active Directory Tümleştirme IdeaScale ile</span><span class="sxs-lookup"><span data-stu-id="48fc8-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="48fc8-104">Bu öğreticide, Azure Active Directory (Azure AD) ile IdeaScale tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="48fc8-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48fc8-105">IdeaScale Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="48fc8-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48fc8-106">IdeaScale erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="48fc8-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="48fc8-107">Otomatik olarak için IdeaScale (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="48fc8-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48fc8-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="48fc8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48fc8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48fc8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48fc8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="48fc8-110">Prerequisites</span></span>

<span data-ttu-id="48fc8-111">Azure AD tümleştirme IdeaScale ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="48fc8-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="48fc8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="48fc8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48fc8-113">Bir IdeaScale çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="48fc8-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48fc8-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="48fc8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48fc8-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="48fc8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48fc8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="48fc8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48fc8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48fc8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48fc8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="48fc8-118">Scenario description</span></span>
<span data-ttu-id="48fc8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="48fc8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48fc8-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="48fc8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48fc8-121">Galeriden IdeaScale ekleme</span><span class="sxs-lookup"><span data-stu-id="48fc8-121">Adding IdeaScale from the gallery</span></span>
2. <span data-ttu-id="48fc8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="48fc8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="48fc8-123">Galeriden IdeaScale ekleme</span><span class="sxs-lookup"><span data-stu-id="48fc8-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="48fc8-124">Azure AD IdeaScale tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden IdeaScale eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="48fc8-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48fc8-125">**Galeriden IdeaScale eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="48fc8-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48fc8-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="48fc8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48fc8-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48fc8-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="48fc8-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="48fc8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="48fc8-133">Arama kutusuna **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-133">In the search box, type **IdeaScale**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="48fc8-135">Sonuçlar panelinde seçin **IdeaScale**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="48fc8-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48fc8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="48fc8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48fc8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı IdeaScale ile test etme</span><span class="sxs-lookup"><span data-stu-id="48fc8-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="48fc8-139">Tekli çalışmaya oturum için Azure AD IdeaScale karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="48fc8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="48fc8-140">Diğer bir deyişle, bir Azure AD kullanıcısının IdeaScale ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="48fc8-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="48fc8-141">IdeaScale içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="48fc8-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48fc8-142">Yapılandırma ve Azure AD çoklu oturum açma IdeaScale ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="48fc8-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48fc8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="48fc8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48fc8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="48fc8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48fc8-145">**[Bir IdeaScale test kullanıcısı oluşturma](#creating-an-ideascale-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı IdeaScale sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="48fc8-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="48fc8-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="48fc8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48fc8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="48fc8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48fc8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="48fc8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48fc8-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma IdeaScale uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="48fc8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="48fc8-150">**Azure AD çoklu oturum açma ile IdeaScale yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="48fc8-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="48fc8-151">Azure portalında üzerinde **IdeaScale** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="48fc8-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="48fc8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="48fc8-155">Üzerinde **IdeaScale etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48fc8-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="48fc8-157">a.</span><span class="sxs-lookup"><span data-stu-id="48fc8-157">a.</span></span> <span data-ttu-id="48fc8-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="48fc8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="48fc8-159">b.</span><span class="sxs-lookup"><span data-stu-id="48fc8-159">b.</span></span> <span data-ttu-id="48fc8-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="48fc8-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="48fc8-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="48fc8-161">These values are not real.</span></span> <span data-ttu-id="48fc8-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="48fc8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="48fc8-163">Kişi [IdeaScale istemci destek ekibi](http://support.ideascale.com/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="48fc8-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="48fc8-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="48fc8-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="48fc8-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="48fc8-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48fc8-168">Üzerinde **IdeaScale yapılandırma** 'yi tıklatın **yapılandırma IdeaScale** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="48fc8-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="48fc8-169">Kopya **Sign-Out URL ve SAML varlık kimliği** gelen **hızlı başvuru bölümünde**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="48fc8-171">Farklı web tarayıcısı penceresinde IdeaScale şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="48fc8-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="48fc8-172">Git **topluluk ayarları**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="48fc8-173">![Topluluk ayarları](./media/active-directory-saas-ideascale-tutorial/ic790847.png "topluluk ayarları")</span><span class="sxs-lookup"><span data-stu-id="48fc8-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="48fc8-174">Git **güvenlik \> tek oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="48fc8-175">![Çoklu oturum açma ayarları](./media/active-directory-saas-ideascale-tutorial/ic790848.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="48fc8-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="48fc8-176">Olarak **çoklu oturum açma türü**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="48fc8-177">![Oturum açma türü tek](./media/active-directory-saas-ideascale-tutorial/ic790849.png "tek oturum açma türü")</span><span class="sxs-lookup"><span data-stu-id="48fc8-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="48fc8-178">Üzerinde **çoklu oturum açma ayarları** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48fc8-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="48fc8-179">![Çoklu oturum açma ayarları](./media/active-directory-saas-ideascale-tutorial/ic790850.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="48fc8-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="48fc8-180">a.</span><span class="sxs-lookup"><span data-stu-id="48fc8-180">a.</span></span> <span data-ttu-id="48fc8-181">İçinde **SAML IDP varlık kimliği** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="48fc8-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="48fc8-182">b.</span><span class="sxs-lookup"><span data-stu-id="48fc8-182">b.</span></span> <span data-ttu-id="48fc8-183">Azure Portalı'ndan indirilen meta veri dosyasının içeriğini kopyalayın ve yapıştırın **SAML IDP meta veri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="48fc8-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="48fc8-184">c.</span><span class="sxs-lookup"><span data-stu-id="48fc8-184">c.</span></span> <span data-ttu-id="48fc8-185">İçinde **oturum kapatma başarı URL** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="48fc8-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="48fc8-186">d.</span><span class="sxs-lookup"><span data-stu-id="48fc8-186">d.</span></span> <span data-ttu-id="48fc8-187">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="48fc8-188">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="48fc8-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48fc8-189">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="48fc8-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48fc8-190">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48fc8-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48fc8-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="48fc8-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="48fc8-192">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="48fc8-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="48fc8-194">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="48fc8-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48fc8-195">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="48fc8-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48fc8-197">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48fc8-199">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="48fc8-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48fc8-201">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48fc8-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48fc8-203">a.</span><span class="sxs-lookup"><span data-stu-id="48fc8-203">a.</span></span> <span data-ttu-id="48fc8-204">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48fc8-205">b.</span><span class="sxs-lookup"><span data-stu-id="48fc8-205">b.</span></span> <span data-ttu-id="48fc8-206">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="48fc8-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48fc8-207">c.</span><span class="sxs-lookup"><span data-stu-id="48fc8-207">c.</span></span> <span data-ttu-id="48fc8-208">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48fc8-209">d.</span><span class="sxs-lookup"><span data-stu-id="48fc8-209">d.</span></span> <span data-ttu-id="48fc8-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="48fc8-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="48fc8-211">Bir IdeaScale test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="48fc8-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="48fc8-212">Azure AD kullanıcıların IdeaScale oturum etkinleştirmek için bunlar içinde IdeaScale için hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="48fc8-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="48fc8-213">IdeaScale söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="48fc8-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="48fc8-214">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="48fc8-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="48fc8-215">Oturum, **IdeaScale** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="48fc8-215">Log in to your **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="48fc8-216">Git **topluluk ayarları**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="48fc8-217">![Topluluk ayarları](./media/active-directory-saas-ideascale-tutorial/ic790847.png "topluluk ayarları")</span><span class="sxs-lookup"><span data-stu-id="48fc8-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="48fc8-218">Git **temel ayarları \> üye yönetim**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-218">Go to **Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="48fc8-219">Tıklatın **üye ekleme**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="48fc8-220">![Üye yönetim](./media/active-directory-saas-ideascale-tutorial/ic790852.png "üye Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="48fc8-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="48fc8-221">Yeni Üye Ekle bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48fc8-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="48fc8-222">![Yeni üye eklemek](./media/active-directory-saas-ideascale-tutorial/ic790853.png "yeni üye ekleme")</span><span class="sxs-lookup"><span data-stu-id="48fc8-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="48fc8-223">a.</span><span class="sxs-lookup"><span data-stu-id="48fc8-223">a.</span></span> <span data-ttu-id="48fc8-224">İçinde **e-posta adresleri** metin kutusuna, kullanmak istediğiniz sağlamak için geçerli bir AAD hesabıyla e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="48fc8-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="48fc8-225">b.</span><span class="sxs-lookup"><span data-stu-id="48fc8-225">b.</span></span> <span data-ttu-id="48fc8-226">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="48fc8-227">Azure Active Directory hesap sahibi etkin duruma gelmesi hesabı onaylamak için bir bağlantı içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="48fc8-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="48fc8-228">API sağlama AAD kullanıcı hesaplarına IdeaScale tarafından sağlanan veya herhangi diğer IdeaScale kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48fc8-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48fc8-229">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="48fc8-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48fc8-230">Bu bölümde, Britta IdeaScale için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="48fc8-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="48fc8-232">**IdeaScale için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="48fc8-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="48fc8-233">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="48fc8-235">Uygulamalar listesinde **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-235">In the applications list, select **IdeaScale**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="48fc8-237">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="48fc8-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="48fc8-239">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="48fc8-239">Click **Add** button.</span></span> <span data-ttu-id="48fc8-240">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48fc8-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="48fc8-242">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="48fc8-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="48fc8-243">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48fc8-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48fc8-244">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48fc8-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48fc8-245">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="48fc8-245">Testing single sign-on</span></span>


<span data-ttu-id="48fc8-246">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="48fc8-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48fc8-247">Erişim paneli IdeaScale parçasında tıklattığınızda, otomatik olarak IdeaScale uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="48fc8-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48fc8-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="48fc8-248">Additional resources</span></span>

* [<span data-ttu-id="48fc8-249">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="48fc8-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48fc8-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="48fc8-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

