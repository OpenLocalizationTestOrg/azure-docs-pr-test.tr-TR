---
title: "aaaManage erişim ve izinleri RBAC - Azure RBAC ile | Microsoft Docs"
description: "Erişim Yönetimi'nde hello Azure portalında Azure rol tabanlı erişim denetimi kullanmaya başlayın. Rol atamaları tooassign izinleri dizininizde kullanın."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>Hello Azure portal'ın rol tabanlı erişim denetimi ile çalışmaya başlama
Güvenlik odaklı şirketler çalışanlar gereksinim duydukları hello tam izinleri vermiş odaklanmanız gerekir. Çok fazla izinleri bir hesap tooattackers getirebilir. Çok az izinleri anlamına gelir çalışanlar verimli bir şekilde işlerini alınamıyor. Azure rol tabanlı erişim denetimi (RBAC), Azure için ayrıntılı erişim yönetimi sunarak bu sorunu gidermeye yardımcı olur.

RBAC kullanarak, ekibiniz içinde görevleri kurabilmeleri ve tooperform işlerini gereksinim yalnızca hello miktarını erişim toousers verin. Kısıtlanmamış izinlerini herkes vermek yerine, Azure aboneliği veya kaynakları yalnızca belirli eylemleri izin verebilirsiniz. Örneğin, kullanım RBAC toolet bir çalışan bir Abonelikteki sanal makineleri yönetmek için başka yönetebilirsiniz sırada SQL hello içinde aynı veritabanları abonelik.

## <a name="basics-of-access-management-in-azure"></a>Azure erişim yönetimi temelleri
Her Azure aboneliği bir Azure Active Directory (AD) dizin ile ilişkilendirilir. Kullanıcılar, gruplar ve uygulamalar bu dizinden hello Azure aboneliği kaynaklarında yönetebilirsiniz. Hello Azure portal, Azure komut satırı araçları ve Azure Management API'leri kullanılarak bu erişim hakları atayın.

Merhaba uygun RBAC rolü toousers, gruplar ve uygulamalar belirli bir kapsamda atayarak erişim sağla. bir rol ataması Hello kapsamını bir abonelik, bir kaynak grubu veya tek bir kaynak olabilir. Bir üst kapsamda atanan bir rol, ayrıca içerdiği toohello alt erişim verir. Örneğin, erişim tooa kaynak grubuna sahip bir kullanıcı, Web siteleri, sanal makineler ve alt ağlar gibi içerdiği tüm hello kaynakları yönetebilir.

![İlişki Azure Active Directory öğeleri arasında - diyagram](./media/role-based-access-control-what-is/rbac_aad.png)

atadığınız hello RBAC rolü bu kapsamı içinde hangi kaynaklara hello kullanıcı, Grup veya uygulama yönetebilirsiniz belirler.

## <a name="built-in-roles"></a>Yerleşik roller
Azure RBAC tooall kaynak türleri geçerli üç temel rol vardır:

* **Sahibi** hello sağ toodelegate erişim tooothers dahil olmak üzere tam erişim tooall kaynaklara sahip.
* **Katkıda bulunan** olabilir oluşturun ve tüm türlerini Azure kaynaklarını yönetmek ancak erişim tooothers veremezsiniz.
* **Okuyucu** mevcut Azure kaynaklarını görüntüleyebilirsiniz.

azure'da hello RBAC rollerin Hello rest belirli Azure kaynaklarının yönetimini sağlar. Örneğin, hello sanal makine katkıda bulunan rolü hello kullanıcı toocreate verir ve sanal makineleri yönetme. Bunları erişim toohello sanal ağ vermez veya sanal makine hello hello alt ağa bağlanır. 

[RBAC yerleşik rolleri](role-based-access-built-in-roles.md) listeleri hello rolleri Azure üzerinde kullanılabilir. Merhaba işlemler ve her yerleşik rol toousers verir kapsam belirtir. Daha fazla denetim için kendi rolleri toodefine arıyorsanız, bkz. nasıl toobuild [Azure rbac'de özel roller](role-based-access-control-custom-roles.md).

## <a name="resource-hierarchy-and-access-inheritance"></a>Kaynak hiyerarşisi ve erişim devralma
* Her **abonelik** Azure'da tooonly bir dizine ait. (Ancak her dizin birden fazla aboneliğiniz olabilir.)
* Her **kaynak grubu** tooonly bir aboneliğe ait.
* Her **kaynak** tooonly bir kaynak grubuna ait.

Üst kapsamların vermek erişim alt kapsamların devralınır. Örneğin:

* Merhaba okuyucu rolü tooan Azure AD grubunun hello abonelik kapsamında atayın. Bu grubun üyeleri Hello her kaynak grubu ve kaynak hello abonelikte görüntüleyebilirsiniz.
* Merhaba katkıda bulunan rolü tooan uygulaması hello kaynak grubu kapsamda atayın. Bu kaynak grubu, ancak diğer kaynak gruplar hello Abonelikteki tüm türlerinin kaynakları yönetebilir.

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>Azure RBAC Klasik abonelik yöneticileri karşılaştırması
Klasik abonelik yöneticileri ve ortak yöneticileri tam erişim toohello Azure aboneliği sahiptir. Hello kullanarak kaynakları yönetebilir [Azure portal](https://portal.azure.com) Azure Resource Manager API'leri veya hello [Klasik Azure portalı](https://manage.windowsazure.com) ve Azure Klasik dağıtım modeli. Merhaba RBAC modelinde, Klasik yöneticileri hello abonelik kapsamında hello sahip rolü atanır.

Yalnızca Azure portal hello ve yeni Azure Resource Manager API'leri desteği Azure RBAC hello. Kullanıcılar ve RBAC rolleri atanmış uygulamalar hello Klasik Yönetim portalını ve hello Azure Klasik dağıtım modeli kullanamazsınız.

## <a name="authorization-for-management-vs-data-operations"></a>Veri işlemleri ve yönetimi için yetkilendirme
Azure RBAC destekleyen yönetim işlemlerini Azure kaynaklarında hello yalnızca Azure portalı ve Azure Resource Manager API'leri hello. Azure kaynakları için tüm veri düzeyi işlemleri yetkilendirilemiyor. Örneğin, birisi yetkilendirebilir toomanage depolama hesapları, ancak toohello bloblarını desteklemez veya bir depolama hesabı içindeki tabloları. Benzer şekilde, bir SQL veritabanı yönetilebilir, ancak içindeki tabloları hello değil.

## <a name="next-steps"></a>Sonraki Adımlar
* Kullanmaya başlama [hello Azure portalı içinde rol tabanlı erişim denetimi](role-based-access-control-configure.md).
* Merhaba bkz [RBAC yerleşik rolleri](role-based-access-built-in-roles.md)
* Kendiniz için [Azure RBAC'de özel roller](role-based-access-control-custom-roles.md) tanımlama
