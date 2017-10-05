---
title: "Azure yönetim API sertifikası karşıya | Microsoft Docs"
description: "Athe yönetim API sertifikası için Klasik Azure portalı karşıya öğrenin."
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
ms.openlocfilehash: 9dc438e927acd9aef38f06807fabf3dda9b021c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="4f12f-103">Azure yönetim API'si yönetim sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="4f12f-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="4f12f-104">Yönetim sertifikaları, Azure tarafından sağlanan Klasik dağıtım modeli, kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f12f-104">Management certificates allow you to authenticate with the classic deployment model provided by Azure.</span></span> <span data-ttu-id="4f12f-105">Birçok programlar ve araçlar (örneğin, Visual Studio ya da Azure SDK'sı) yapılandırma ve çeşitli Azure hizmetlerine dağıtımını otomatik hale getirmek için bu sertifikaları kullanacak.</span><span class="sxs-lookup"><span data-stu-id="4f12f-105">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="4f12f-106">Dikkat et!</span><span class="sxs-lookup"><span data-stu-id="4f12f-106">Be careful!</span></span> <span data-ttu-id="4f12f-107">Bu tür bir sertifika ile ilişkili aboneliği yönetmek için kimlik doğrulamasını herkes izin verin.</span><span class="sxs-lookup"><span data-stu-id="4f12f-107">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span>
>
>

<span data-ttu-id="4f12f-108">(Dahil olmak üzere otomatik olarak imzalanan sertifika oluşturma) Azure sertifikalar hakkında daha fazla bilgi isterseniz bkz [Azure Cloud Services sertifikalarına genel bakış](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="4f12f-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="4f12f-109">Aynı zamanda [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) Otomasyon amaçları için istemci kodu doğrulanacak.</span><span class="sxs-lookup"><span data-stu-id="4f12f-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) to authenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="4f12f-110">Bir yönetim sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="4f12f-110">Upload a management certificate</span></span>
<span data-ttu-id="4f12f-111">Bulduktan sonra oluşturulan yönetim sertifikası, (.cer dosyası yalnızca ortak anahtarla) portalına karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="4f12f-111">Once you have a management certificate created, (.cer file with only the public key) you can upload it into the portal.</span></span> <span data-ttu-id="4f12f-112">Sertifika Portalı'nda kullanılabilir olduğunda, eşleşen bir sertifika (özel anahtarı) kimseyle Yönetimi API aracılığıyla bağlanmak ve ilişkili aboneliği için kaynak erişim.</span><span class="sxs-lookup"><span data-stu-id="4f12f-112">When the certificate is available in the portal, anyone with a matching certificate (private key) can connect through the Management API and access the resources for the associated subscription.</span></span>

1. <span data-ttu-id="4f12f-113">[Azure Portal](http://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4f12f-113">Log in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="4f12f-114">Tıklatın **daha fazla hizmet** alt Azure hizmeti listenin seçip **abonelikleri** içinde _genel_ hizmeti grubu.</span><span class="sxs-lookup"><span data-stu-id="4f12f-114">Click **More services** at the bottom Azure service list, then select **Subscriptions** in the _General_ service group.</span></span>

    ![Abonelik menüsü](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="4f12f-116">Sertifika ile ilişkilendirmek istediğiniz için doğru aboneliğin seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4f12f-116">Make sure to select the correct subscription that you want to associate with the certificate.</span></span>     
4. <span data-ttu-id="4f12f-117">Doğru abonelik seçtikten sonra basın **yönetim sertifikaları** içinde _ayarları_ grubu.</span><span class="sxs-lookup"><span data-stu-id="4f12f-117">After you have selected the correct subscription, press **Management certificates** in the _Settings_ group.</span></span>

    ![Ayarlar](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="4f12f-119">Tuşuna **karşıya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4f12f-119">Press the **Upload** button.</span></span>

    ![Sertifikalar sayfasında karşıya yükle](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="4f12f-121">İletişim bilgileri ve tuşuna doldurmak **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="4f12f-121">Fill out the dialog information and press **Upload**.</span></span>

    ![Ayarlar](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="4f12f-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f12f-123">Next steps</span></span>
<span data-ttu-id="4f12f-124">Bir aboneliği ile ilişkili bir yönetim sertifikası sahip olduğunuza göre (yerel olarak eşleşen sertifika yükledikten sonra) programlı olarak bağlanabileceğiniz [Klasik dağıtım modeli REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) ve otomatik hale getirme Ayrıca bu abonelikle ilişkili çeşitli Azure kaynakları.</span><span class="sxs-lookup"><span data-stu-id="4f12f-124">Now that you have a management certificate associated with a subscription, you can (after you have installed the matching certificate locally) programmatically connect to the [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate the various Azure resources that are also associated with that subscription.</span></span>
