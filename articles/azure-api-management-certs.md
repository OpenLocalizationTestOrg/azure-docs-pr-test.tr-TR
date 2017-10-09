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
# <a name="upload-an-azure-management-api-management-certificate"></a>Azure yönetim API'si yönetim sertifikasını karşıya yükle
Yönetim sertifikaları, tooauthenticate hello Klasik dağıtım modeliyle Azure tarafından sağlanan izin verin. Birçok programlar ve araçlar (örneğin, Visual Studio veya hello Azure SDK'sı) Bu sertifika tooautomate yapılandırması ve çeşitli Azure hizmetlerine dağıtımını kullanın. 

> [!WARNING]
> Dikkat et! Bu tür bir sertifika ile kimliklerini doğrulayan herkes izin bunların ilişkili toomanage hello abonelik.
>
>

(Dahil olmak üzere otomatik olarak imzalanan sertifika oluşturma) Azure sertifikalar hakkında daha fazla bilgi isterseniz bkz [Azure Cloud Services sertifikalarına genel bakış](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

Aynı zamanda [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate Otomasyon amaçları için istemci kodu.

## <a name="upload-a-management-certificate"></a>Bir yönetim sertifikasını karşıya yükle
Bulduktan sonra oluşturulan yönetim sertifikası, (.cer dosyası yalnızca hello ortak anahtarla) hello portalına karşıya yükleyebilir. Merhaba sertifika hello Portalı'nda kullanılabilir olduğunda, herkesin (özel anahtarı) eşleşen bir sertifika ile ilişkili hello abonelik hello yönetim API'si ve erişim hello kaynakları aracılığıyla bağlanabilir.

1. İçinde toohello oturum [Azure portal](http://portal.azure.com).
2. Tıklatın **daha fazla hizmet** hello alt Azure hizmeti listenin seçip **abonelikleri** hello içinde _genel_ hizmeti grubu.

    ![Abonelik menüsü](./media/azure-api-management-certs/subscriptions_menu.png)

3. Tooselect hello hello sertifikayla tooassociate istediğiniz doğru aboneliğin emin olun.     
4. Merhaba doğru abonelik seçtikten sonra basın **yönetim sertifikaları** hello içinde _ayarları_ grubu.

    ![Ayarlar](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Tuşuna hello **karşıya** düğmesi.

    ![Sertifikalar sayfasında karşıya yükle](./media/azure-api-management-certs/certificates_page.png)
6. Merhaba iletişim bilgileri ve tuşuna doldurmak **karşıya**.

    ![Ayarlar](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Sonraki adımlar
Bir aboneliği ile ilişkili bir yönetim sertifikası sahip olduğunuza göre (sertifika yerel olarak eşleşen hello yükledikten sonra), program aracılığıyla toohello bağlanabilirsiniz [Klasik dağıtım modeli REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) ve otomatik hale getirme Ayrıca bu abonelikle ilişkili çeşitli Azure kaynaklarını hello.
