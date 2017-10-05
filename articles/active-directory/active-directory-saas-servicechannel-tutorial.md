---
title: "Öğretici: Azure Active Directory Tümleştirme ile ServiceChannel | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile ServiceChannel arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 7e1dad18ff0ae9a9102b789b2cb32e7b96ed3d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="fd64a-103">Öğretici: Azure Active Directory Tümleştirme ServiceChannel ile</span><span class="sxs-lookup"><span data-stu-id="fd64a-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="fd64a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile ServiceChannel tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fd64a-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fd64a-105">ServiceChannel Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fd64a-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fd64a-106">ServiceChannel erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fd64a-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="fd64a-107">Otomatik olarak için ServiceChannel (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fd64a-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fd64a-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="fd64a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="fd64a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fd64a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd64a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fd64a-110">Prerequisites</span></span>

<span data-ttu-id="fd64a-111">Azure AD tümleştirme ServiceChannel ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="fd64a-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="fd64a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fd64a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fd64a-113">Bir ServiceChannel çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="fd64a-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fd64a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fd64a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fd64a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fd64a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fd64a-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd64a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="fd64a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd64a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fd64a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fd64a-118">Scenario description</span></span>
<span data-ttu-id="fd64a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fd64a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fd64a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fd64a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fd64a-121">Galeriden ServiceChannel ekleme</span><span class="sxs-lookup"><span data-stu-id="fd64a-121">Adding ServiceChannel from the gallery</span></span>
2. <span data-ttu-id="fd64a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fd64a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="fd64a-123">Galeriden ServiceChannel ekleme</span><span class="sxs-lookup"><span data-stu-id="fd64a-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="fd64a-124">Azure AD ServiceChannel tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden ServiceChannel eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd64a-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fd64a-125">**Galeriden ServiceChannel eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fd64a-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fd64a-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fd64a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fd64a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fd64a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="fd64a-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd64a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="fd64a-133">Arama kutusuna **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-133">In the search box, type **ServiceChannel**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="fd64a-135">Sonuçlar panelinde seçin **ServiceChannel**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd64a-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fd64a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fd64a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fd64a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ServiceChannel sınayın.</span><span class="sxs-lookup"><span data-stu-id="fd64a-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fd64a-139">Tekli çalışmaya oturum için Azure AD ServiceChannel karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="fd64a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="fd64a-140">Diğer bir deyişle, bir Azure AD kullanıcısının ServiceChannel ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd64a-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="fd64a-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** ServiceChannel içinde.</span><span class="sxs-lookup"><span data-stu-id="fd64a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="fd64a-142">Yapılandırma ve Azure AD çoklu oturum açma ServiceChannel ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fd64a-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fd64a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fd64a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fd64a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="fd64a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fd64a-145">**[ServiceChannel test kullanıcısı oluşturma](#creating-a-servicechannel-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="fd64a-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="fd64a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fd64a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fd64a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fd64a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fd64a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fd64a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fd64a-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma ServiceChannel uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fd64a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="fd64a-150">**Azure AD çoklu oturum açma ile ServiceChannel yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fd64a-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="fd64a-151">Azure Yönetim Portalı'nda üzerinde **ServiceChannel** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="fd64a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fd64a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="fd64a-155">Üzerinde **ServiceChannel etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fd64a-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="fd64a-157">a.</span><span class="sxs-lookup"><span data-stu-id="fd64a-157">a.</span></span> <span data-ttu-id="fd64a-158">İçinde **tanımlayıcısı** metin değeri olarak yazın:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="fd64a-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="fd64a-159">b.</span><span class="sxs-lookup"><span data-stu-id="fd64a-159">b.</span></span> <span data-ttu-id="fd64a-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="fd64a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fd64a-161">Lütfen bu gerçek değerlerin olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fd64a-161">Please note that these are not the real values.</span></span> <span data-ttu-id="fd64a-162">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd64a-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="fd64a-163">Burada dizesinin benzersiz değeri tanımlayıcıda kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="fd64a-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="fd64a-164">Kişi [ServiceChannel destek ekibi](https://servicechannel.zendesk.com/hc/en-us) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="fd64a-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

4. <span data-ttu-id="fd64a-165">SAML belirteci öznitelikleri yapılandırmanıza özel öznitelik eşlemelerini ekleyin gerektiren belirli bir biçimde SAML onaylar ServiceChannel uygulamanızı bekliyor.</span><span class="sxs-lookup"><span data-stu-id="fd64a-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="fd64a-166">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="fd64a-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="fd64a-167">**NameIdentifier (kullanıcı tanımlayıcısı)** yalnızca zorunlu talebi ve varsayılan değer **user.userprincipalname** ancak ServiceChannel bekliyor bu ile eşlenecek **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="fd64a-168">Yalnızca zaman içinde kullanıcı sağlamayı etkinleştirin planlıyorsanız, aşağıda gösterildiği gibi aşağıdaki talep eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="fd64a-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="fd64a-169">**Rol** talep eşlenmesi gerekiyor **user.assignedroles** kullanıcı rolünü içerir.</span><span class="sxs-lookup"><span data-stu-id="fd64a-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="fd64a-170">ServiceChannel Kılavuzu başvurabilir [burada](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) talepler hakkında daha fazla yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="fd64a-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="fd64a-172">Lütfen tıklatın [burada](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) nasıl yapılandırılacağını öğrenmek için **rol** Azure AD'de</span><span class="sxs-lookup"><span data-stu-id="fd64a-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) to know how to configure **Role** in Azure AD</span></span>

5. <span data-ttu-id="fd64a-173">İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve özniteliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fd64a-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="fd64a-174">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="fd64a-174">Attribute Name</span></span> | <span data-ttu-id="fd64a-175">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="fd64a-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="fd64a-176">Rol</span><span class="sxs-lookup"><span data-stu-id="fd64a-176">Role</span></span>| <span data-ttu-id="fd64a-177">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="fd64a-177">user.assignedroles</span></span> |

    <span data-ttu-id="fd64a-178">a.</span><span class="sxs-lookup"><span data-stu-id="fd64a-178">a.</span></span> <span data-ttu-id="fd64a-179">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd64a-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="fd64a-182">b.</span><span class="sxs-lookup"><span data-stu-id="fd64a-182">b.</span></span> <span data-ttu-id="fd64a-183">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="fd64a-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="fd64a-184">c.</span><span class="sxs-lookup"><span data-stu-id="fd64a-184">c.</span></span> <span data-ttu-id="fd64a-185">Gelen **değeri** listesinde, ilgili satır için gösterilen öznitelik değeri yazın.</span><span class="sxs-lookup"><span data-stu-id="fd64a-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="fd64a-186">d.</span><span class="sxs-lookup"><span data-stu-id="fd64a-186">d.</span></span> <span data-ttu-id="fd64a-187">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="fd64a-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="fd64a-188">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fd64a-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="fd64a-190">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fd64a-190">Click **Save**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fd64a-192">Üzerinde **ServiceChannel yapılandırma** 'yi tıklatın **yapılandırma ServiceChannel** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="fd64a-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fd64a-193">Lütfen unutmayın **SAML Enitity kimliği** gelen **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="fd64a-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

9. <span data-ttu-id="fd64a-194">Çoklu oturum açma yapılandırmak için **ServiceChannel** yan, indirilen göndermek için ihtiyacınız **sertifika (Base64)** ve **SAML varlık kimliği** için [ServiceChannel destek ekibi](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="fd64a-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="fd64a-195">Bunlar bu iki tarafta da ayarlamanızı SAML SSO bağlantınız için kurar.</span><span class="sxs-lookup"><span data-stu-id="fd64a-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fd64a-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd64a-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="fd64a-197">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="fd64a-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="fd64a-199">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fd64a-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fd64a-200">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fd64a-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fd64a-202">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="fd64a-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fd64a-204">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd64a-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fd64a-206">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fd64a-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fd64a-208">a.</span><span class="sxs-lookup"><span data-stu-id="fd64a-208">a.</span></span> <span data-ttu-id="fd64a-209">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fd64a-210">b.</span><span class="sxs-lookup"><span data-stu-id="fd64a-210">b.</span></span> <span data-ttu-id="fd64a-211">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="fd64a-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fd64a-212">c.</span><span class="sxs-lookup"><span data-stu-id="fd64a-212">c.</span></span> <span data-ttu-id="fd64a-213">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fd64a-214">d.</span><span class="sxs-lookup"><span data-stu-id="fd64a-214">d.</span></span> <span data-ttu-id="fd64a-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fd64a-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="fd64a-216">ServiceChannel test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd64a-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="fd64a-217">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar uygulamada otomatik olarak oluşturulacak sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="fd64a-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="fd64a-218">Tam kullanıcı sağlama için temasa [ServiceChannel destek ekibi](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="fd64a-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fd64a-219">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="fd64a-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fd64a-220">Bu bölümde, Britta ServiceChannel için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fd64a-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="fd64a-222">**ServiceChannel için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fd64a-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="fd64a-223">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fd64a-225">Uygulamalar listesinde **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-225">In the applications list, select **ServiceChannel**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="fd64a-227">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fd64a-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="fd64a-229">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fd64a-229">Click **Add** button.</span></span> <span data-ttu-id="fd64a-230">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd64a-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="fd64a-232">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fd64a-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fd64a-233">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd64a-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fd64a-234">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fd64a-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fd64a-235">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fd64a-235">Testing single sign-on</span></span>

<span data-ttu-id="fd64a-236">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="fd64a-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fd64a-237">Erişim paneli ServiceChannel parçasında tıklattığınızda, otomatik olarak ServiceChannel uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="fd64a-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fd64a-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fd64a-238">Additional resources</span></span>

* [<span data-ttu-id="fd64a-239">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="fd64a-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd64a-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fd64a-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png