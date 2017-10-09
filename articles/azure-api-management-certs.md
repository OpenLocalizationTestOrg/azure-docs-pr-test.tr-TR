---
title: "bir Azure yönetim API sertifikası aaaUpload | Microsoft Docs"
description: "Nasıl tooupload athe yönetim API sertifikası Merhaba Klasik Azure portalı öğrenin."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="63726-103">Azure yönetim API'si yönetim sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="63726-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="63726-104">Yönetim sertifikaları, tooauthenticate hello Klasik dağıtım modeliyle Azure tarafından sağlanan izin verin.</span><span class="sxs-lookup"><span data-stu-id="63726-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="63726-105">Birçok programlar ve araçlar (örneğin, Visual Studio veya hello Azure SDK'sı) Bu sertifika tooautomate yapılandırması ve çeşitli Azure hizmetlerine dağıtımını kullanın.</span><span class="sxs-lookup"><span data-stu-id="63726-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="63726-106">Dikkat et!</span><span class="sxs-lookup"><span data-stu-id="63726-106">Be careful!</span></span> <span data-ttu-id="63726-107">Bu tür bir sertifika ile kimliklerini doğrulayan herkes izin bunların ilişkili toomanage hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="63726-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="63726-108">(Dahil olmak üzere otomatik olarak imzalanan sertifika oluşturma) Azure sertifikalar hakkında daha fazla bilgi isterseniz bkz [Azure Cloud Services sertifikalarına genel bakış](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="63726-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="63726-109">Aynı zamanda [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate Otomasyon amaçları için istemci kodu.</span><span class="sxs-lookup"><span data-stu-id="63726-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="63726-110">Bir yönetim sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="63726-110">Upload a management certificate</span></span>
<span data-ttu-id="63726-111">Bulduktan sonra oluşturulan yönetim sertifikası, (.cer dosyası yalnızca hello ortak anahtarla) hello portalına karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="63726-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="63726-112">Merhaba sertifika hello Portalı'nda kullanılabilir olduğunda, herkesin (özel anahtarı) eşleşen bir sertifika ile ilişkili hello abonelik hello yönetim API'si ve erişim hello kaynakları aracılığıyla bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="63726-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="63726-113">İçinde toohello oturum [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="63726-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="63726-114">Tıklatın **daha fazla hizmet** hello alt Azure hizmeti listenin seçip **abonelikleri** hello içinde _genel_ hizmeti grubu.</span><span class="sxs-lookup"><span data-stu-id="63726-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![Abonelik menüsü](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="63726-116">Tooselect hello hello sertifikayla tooassociate istediğiniz doğru aboneliğin emin olun.</span><span class="sxs-lookup"><span data-stu-id="63726-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="63726-117">Merhaba doğru abonelik seçtikten sonra basın **yönetim sertifikaları** hello içinde _ayarları_ grubu.</span><span class="sxs-lookup"><span data-stu-id="63726-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![Ayarlar](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="63726-119">Tuşuna hello **karşıya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="63726-119">Press hello **Upload** button.</span></span>

    ![Sertifikalar sayfasında karşıya yükle](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="63726-121">Merhaba iletişim bilgileri ve tuşuna doldurmak **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="63726-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![Ayarlar](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="63726-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="63726-123">Next steps</span></span>
<span data-ttu-id="63726-124">Bir aboneliği ile ilişkili bir yönetim sertifikası sahip olduğunuza göre (sertifika yerel olarak eşleşen hello yükledikten sonra), program aracılığıyla toohello bağlanabilirsiniz [Klasik dağıtım modeli REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) ve otomatik hale getirme Ayrıca bu abonelikle ilişkili çeşitli Azure kaynaklarını hello.</span><span class="sxs-lookup"><span data-stu-id="63726-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
