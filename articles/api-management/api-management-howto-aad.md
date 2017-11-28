---
title: "Azure Active Directory - Azure API Management kullanarak aaaAuthorize Geliştirici hesapları | Microsoft Docs"
description: "Bilgi nasıl tooauthorize kullanıcıları API Management'te Azure Active Directory kullanarak."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="7a3a9-103">Nasıl tooauthorize Geliştirici kullanarak hesapları Azure API Management'te Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a3a9-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="7a3a9-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7a3a9-104">Overview</span></span>
<span data-ttu-id="7a3a9-105">Bu kılavuz size nasıl tooenable erişim toohello Geliştirici portalı kullanıcıları için Azure Active Directory'den gösterir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="7a3a9-106">Bu kılavuz Ayrıca, Azure Active Directory Kullanıcıları içeren dış grupları ekleyerek toomanage grupları Azure Active Directory Kullanıcıları nasıl hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="7a3a9-107">toocomplete hello adımları bu kılavuzda, ilk Azure Active Directory hangi toocreate bir uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="7a3a9-108">Nasıl tooauthorize Geliştirici kullanarak hesapları Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a3a9-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="7a3a9-109">başlatıldı, tooget tıklatın **yayımcı portalına** hello API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="7a3a9-110">Bu toohello API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-110">This takes you toohello API Management publisher portal.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="7a3a9-112">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="7a3a9-113">Tıklatın **güvenlik** hello gelen **API Management** hello sol ve tıklatın menüsünde **dış kimlikler**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![Dış kimlikler][api-management-security-external-identities]

<span data-ttu-id="7a3a9-115">Tıklatın **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="7a3a9-116">Merhaba Not **tekrar yönlendirme URL'sini** ve hello Klasik Azure portalı, Azure Active Directory tooyour üzerinden geçin.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![Dış kimlikler][api-management-security-aad-new]

<span data-ttu-id="7a3a9-118">Merhaba tıklatın **Ekle** düğmesini toocreate yeni bir Azure Active Directory uygulaması ve seçin **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Yeni bir Azure Active Directory uygulaması ekleyin][api-management-new-aad-application-menu]

<span data-ttu-id="7a3a9-120">Select hello uygulama için bir ad girin **Web uygulaması ve/veya Web API**ve hello İleri düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![Yeni Azure Active Directory uygulaması][api-management-new-aad-application-1]

<span data-ttu-id="7a3a9-122">İçin **oturum açma URL'si**, Geliştirici Portalı oturum açma hello URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="7a3a9-123">Bu örnekte, hello **oturum açma URL'si** olan `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="7a3a9-124">Hello için **uygulama kimliği URL'si**hello varsayılan etki alanı veya özel bir etki alanı hello Azure Active Directory girin ve benzersiz bir dize tooit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="7a3a9-125">Bu örnekte, varsayılan etki alanı hello **https://contoso5api.onmicrosoft.com** hello sonek ile kullanılır **/api** belirtilen.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![Yeni Azure Active Directory uygulama özellikleri][api-management-new-aad-application-2]

<span data-ttu-id="7a3a9-127">Merhaba onay düğmesine toosave'ı tıklatın ve Merhaba uygulaması oluşturup toohello geçiş **yapılandırma** tooconfigure hello yeni uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![Oluşturulan yeni Azure Active Directory uygulaması][api-management-new-aad-app-created]

<span data-ttu-id="7a3a9-129">Birden çok Azure Active dizinleri bu uygulama için kullanılan toobe kullanacaksanız tıklatın **Evet** için **uygulamasıdır çok kiracılı**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="7a3a9-130">Merhaba varsayılandır **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-130">hello default is **No**.</span></span>

![Çok kiracılı uygulama][api-management-aad-app-multi-tenant]

<span data-ttu-id="7a3a9-132">Kopya hello **tekrar yönlendirme URL'sini** hello gelen **Azure Active Directory** hello bölümünü **dış kimlikler** sekmesinde hello yayımcı Portalı'nda ve helloyapıştırma**Yanıt URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![Yanıt URL'si][api-management-aad-reply-url]

<span data-ttu-id="7a3a9-134">Kaydırma toohello alt Merhaba yapılandırma sekmesi, select hello **uygulama izinleri** aşağı açılır ve denetleme **dizin verilerini okuma**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Uygulama izinleri][api-management-aad-app-permissions]

<span data-ttu-id="7a3a9-136">Select hello **temsilci izinleri** aşağı açılır ve denetleme **oturum açmayı etkinleştir ve kullanıcıların profilleri okuma**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Temsilci izinleri][api-management-aad-delegated-permissions]

> <span data-ttu-id="7a3a9-138">Uygulama ve temsilci izinleri hakkında daha fazla bilgi için bkz: [erişme hello grafik API'si][Accessing hello Graph API].</span><span class="sxs-lookup"><span data-stu-id="7a3a9-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="7a3a9-139">Kopya hello **istemci kimliği** toohello Pano.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-139">Copy hello **Client Id** toohello clipboard.</span></span>

![İstemci kimliği][api-management-aad-app-client-id]

<span data-ttu-id="7a3a9-141">Geri toohello yayımcı portalına geçin ve hello Yapıştır **istemci kimliği** hello Azure Active Directory Uygulama yapılandırmasından kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![İstemci kimliği][api-management-client-id]

<span data-ttu-id="7a3a9-143">Geçin geri toohello Azure Active Directory yapılandırması ve hello tıklatın **seçin süresi** hello açılan **anahtarları** bölüm ve bir aralık belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="7a3a9-144">Bu örnekte, **1 yıl** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-144">In this example, **1 year** is used.</span></span>

![Anahtar][api-management-aad-key-before-save]

<span data-ttu-id="7a3a9-146">Tıklatın **kaydetmek** toosave hello yapılandırma ve görüntü hello anahtarı.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="7a3a9-147">Merhaba anahtar toohello panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="7a3a9-148">Bu anahtarı not edin.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-148">Make a note of this key.</span></span> <span data-ttu-id="7a3a9-149">Hello Azure Active Directory yapılandırması penceresini kapattığınızda hello anahtarı yeniden görüntülenemiyor.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![Anahtar][api-management-aad-key-after-save]

<span data-ttu-id="7a3a9-151">Anahtar geri toohello yayımcı portalı ve Yapıştır hello anahtara hello **gizli** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![İstemci parolası][api-management-client-secret]

<span data-ttu-id="7a3a9-153">**Kiracılar izin** erişim toohello hello API Management hizmet örneği, API hangi dizinleri sahip belirtir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="7a3a9-154">Merhaba toogrant erişim istediğiniz Azure Active Directory örnekleri toowhich Hello etki alanları belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="7a3a9-155">Birden çok etki alanı, satır başı, boşluk veya virgülle ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![İzin verilen kiracılar][api-management-client-allowed-tenants]


<span data-ttu-id="7a3a9-157">Yapılandırma belirtilen Hello istenen sonra tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-157">Once hello desired configuration is specified, click **Save**.</span></span>

![Kaydet][api-management-client-allowed-tenants-save]

<span data-ttu-id="7a3a9-159">Azure Active Directory oturum açabilir toohello Geliştirici Portalı'nda hello adımları izleyerek hello hello kullanıcılar Hello değişiklikler kaydedildikten sonra belirtilen [toohello Geliştirici portalında bir Azure Active Directory hesabı kullanarak oturum] [Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="7a3a9-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="7a3a9-160">Birden çok etki alanı hello belirtilebilir **izin kiracılar** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="7a3a9-161">Merhaba uygulaması kaydedildiği hello özgün etki alanı farklı bir etki alanından herhangi bir kullanıcı oturum önce hello farklı etki alanının genel yönetici dizin verilerini hello uygulama tooaccess izni vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="7a3a9-162">toogrant izni hello genel yönetici çok gitmesini`https://<URL of your developer portal>/aadadminconsent` (örneğin, https://contoso.portal.azure-api.net/aadadminconsent) hello toogive erişim tooand istedikleri Active Directory Kiracı hello etki alanı adındaki türünü gönderme tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="7a3a9-163">Merhaba aşağıdaki örnek, bir genel yönetici `miaoaad.onmicrosoft.com` toogive izin toothis belirli Geliştirici Portalı çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![İzinler][api-management-aad-consent]

<span data-ttu-id="7a3a9-165">Merhaba sonraki ekranda, istendiğinde tooconfirm hello izin vermiş hello genel yönetici olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![İzinler][api-management-permissions-form]

> <span data-ttu-id="7a3a9-167">İçinde toolog izinleri önce genel bir yönetici tarafından verilen genel olmayan bir yönetici çalışırsa hello oturum açma denemesi başarısız olur ve hata ekranı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="7a3a9-168">Tooadd dış Azure Active Directory Grup nasıl</span><span class="sxs-lookup"><span data-stu-id="7a3a9-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="7a3a9-169">Kullanıcılar Azure Active Directory erişimi etkinleştirdikten sonra API Management toomore Azure Active Directory gruplarına hello geliştiriciler hello grubundaki hello ilişkilendirme istenen hello ürünleri ile kolayca yönetmenize ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="7a3a9-170">tooconfigure dış bir Azure Active Directory grubu olan hello Azure Active Directory ilk hello kimlikleri sekmesinde hello önceki bölümdeki hello yordamı izleyerek yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="7a3a9-171">Dış Azure Active Directory grupları hello eklenen **görünürlük** toogrant erişim toohello grubu istediğiniz hello ürün sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="7a3a9-172">Tıklatın **ürünleri**ve ardından hello istenen ürün hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![Ürünü yapılandırma][api-management-configure-product]

<span data-ttu-id="7a3a9-174">Geçiş toohello **görünürlük** sekmesine ve tıklayın **Azure Active Directory grupları Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Grupları Ekle][api-management-add-groups]

<span data-ttu-id="7a3a9-176">Select hello **Azure Active Directory Kiracısı** hello aşağı açılan liste ve hello istenen hello grubunda sonra tür hello adını **grupları** toobe metin kutusuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![Grup Seç][api-management-select-group]

<span data-ttu-id="7a3a9-178">Bu grup adı hello bulunabilir **grupları** hello aşağıdaki örnekte gösterildiği gibi Azure Active Directory için liste.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Azure Active Directory grupları listesi][api-management-aad-groups-list]

<span data-ttu-id="7a3a9-180">Tıklatın **Ekle** toovalidate hello grup adı ve hello grubunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="7a3a9-181">Bu örnekte, hello **Contoso 5 geliştiriciler** dış grubuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![Eklenen grubu][api-management-aad-group-added]

<span data-ttu-id="7a3a9-183">Tıklatın **kaydetmek** toosave hello yeni Grup Seçimi.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="7a3a9-184">Bir Azure Active Directory grubu bir üründen yapılandırıldıktan sonra kullanılabilir toobe üzerinde hello işaretli olduğu **görünürlük** sekmesini hello diğer ürünleri hello API Management hizmet örneği.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="7a3a9-185">tooreview ve bunlar eklendikten sonra dış gruplar hello hello grubundan hello adını hello özelliklerini yapılandıramadı **grupları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![Grupları yönetme][api-management-groups]

<span data-ttu-id="7a3a9-187">Buradan hello düzenleyebilirsiniz **adı** ve hello **açıklama** hello grubunun.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![Grubu Düzenle][api-management-edit-group]

<span data-ttu-id="7a3a9-189">Merhaba kullanıcılardan yapılandırılmış Azure Active Directory toohello Geliştirici Portalı ve görünümünde oturum ve görünürlük bölümden hello hello yönergeleri takip ederek sahip oldukları tooany grupları abone.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="7a3a9-190">Nasıl toolog toohello Geliştirici portalında bir Azure Active Directory hesabı kullanarak</span><span class="sxs-lookup"><span data-stu-id="7a3a9-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="7a3a9-191">Merhaba önceki bölümlerde, yapılandırılmış bir Azure Active Directory hesabı kullanarak hello Geliştirici Portalı içine toolog hello kullanarak yeni bir tarayıcı penceresi açın **oturum açma URL'si** hello Active Directory Uygulama Yapılandırması ve tıklatın **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Geliştirici Portalı][api-management-dev-portal-signin]

<span data-ttu-id="7a3a9-193">Azure Active Directory'yi hello kullanıcılar birini Hello kimlik bilgilerini girin ve tıklayın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![Oturum aç][api-management-aad-signin]

<span data-ttu-id="7a3a9-195">Ek bilgileri gerekiyorsa, Kayıt formuyla istenebilir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="7a3a9-196">Merhaba kayıt formunu tamamladıktan ve tıklayın **kaydolun**.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-196">Complete hello registration form and click **Sign up**.</span></span>

![Kayıt][api-management-complete-registration]

<span data-ttu-id="7a3a9-198">Kullanıcı artık hello Geliştirici Portalı, API Management hizmet örneğinizin içine kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="7a3a9-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

![Kayıt tamamlandı][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

