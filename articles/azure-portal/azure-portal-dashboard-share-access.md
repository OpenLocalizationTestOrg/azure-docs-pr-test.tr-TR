---
title: "aaaShare Azure RBAC kullanarak portalı panoları | Microsoft Docs"
description: "Bu makalede nasıl tooshare panosunda bir hello Azure portalında rol tabanlı erişim denetimi kullanarak açıklanmaktadır."
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a>Rol tabanlı erişim denetimi kullanarak Azure panoları paylaşmak
Bir Pano yapılandırdıktan sonra yayımlayabilir ve kuruluşunuzdaki diğer kullanıcılarla paylaşmak. Başkalarının izin tooview Azure kullanarak panonuz [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md). Bir kullanıcı veya grup kullanıcılar tooa rolü atayın ve bu rol kullanıcılarla değiştirebilir veya görüntüleyebilirsiniz hello yayımlanan Pano olup olmadığını tanımlar. 

Tüm yayımlanan panolar Azure kaynakları yönetilebilir öğeleri aboneliğinizi içinde mevcut ve bir kaynak grubunda bulunan yani uygulanır.  Bir erişim denetimi açısından bakıldığında, panolar sanal makine ya da bir depolama hesabı gibi başka kaynaklar gereksinimlerinden farklı değildir.

> [!TIP]
> Tek tek döşeme hello Panoda görüntüledikleri hello kaynaklara bağlı kendi erişim denetimi gereksinimlerine uygulayın.  Bu nedenle, geniş çapta hala tek tek döşeme hello verilerini korurken paylaşılan bir Pano tasarlayabilirsiniz.
> 
> 

## <a name="understanding-access-control-for-dashboards"></a>Panolar için erişim Denetimi'ni anlama
Rol tabanlı erişim denetimi (RBAC) birlikte kullanıcıların tooroles kapsamının üç farklı düzeylerde atayabilirsiniz:

* aboneliği
* kaynak grubu
* Kaynak

Merhaba izinler atadığınız toohello kaynak aşağı abonelikten devralınır. Merhaba yayımlanan Pano bir kaynaktır. Bu nedenle, aynı zamanda hello yayımlanan Pano için çalışan atanan kullanıcılar tooroles hello abonelik için zaten sahip olabilir. 

Bir örnek verilmiştir.  Bir Azure aboneliğiniz varsa ve çeşitli ekibinizin üyeleri hello rollerini atamış olduğunuz düşünelim **sahibi**, **katkıda bulunan**, veya **okuyucu** hello abonelik için. Sahipler veya katkıda bulunanlar kullanıcılar mümkün toolist, görünüm olan, oluşturmak, değiştirmek veya hello abonelik içindeki panoları silin.  Okuyucular kullanıcılar mümkün toolist ve görünüm panolar, ancak değiştirin veya silin.  Okuyucu erişimi olan kullanıcılar olan mümkün toomake yerel düzenlemeleri tooa yayımlanan Pano (gibi bir sorun gidermede), ancak şu toopublish bu değişiklikleri geri toohello sunucu.  Bunlar hello seçeneği toomake hello panonun özel bir kopyasını kendileri için olacaktır

Bununla birlikte, birçok panolar veya tooan tek tek Pano içeren izinleri toohello kaynak grubunu da atayabilirsiniz. Örneğin, bir kullanıcı grubuna izinleri hello abonelik ancak büyük erişim tooa belirli Pano sınırlı olmalıdır, karar verebilirsiniz. Bu Pano için bu kullanıcıların tooa rolü atayın. 

## <a name="publish-dashboard"></a>Pano yayımlama
Şimdi, aboneliğinizde kullanıcı grubuyla tooshare istediğiniz bir Pano yapılandırmayı tamamladıktan varsayalım. Depolama yöneticileri adlı özel bir grup Hello adımları tarif, ancak ne olursa olsun ister misiniz grubunuzun adı verebilirsiniz. Bir Active Directory grubu oluşturma ve kullanıcılara toothat grup ekleme hakkında daha fazla bilgi için bkz: [Azure Active Directory içinde grupları yönetme](../active-directory/active-directory-accessmanagement-manage-groups.md).

1. Merhaba panosunda seçin **paylaşımı**.
   
     ![Paylaşımı seçin](./media/azure-portal-dashboard-share-access/select-share.png)
2. Erişim vermeden önce hello Pano yayımlamanız gerekir. Varsayılan olarak, yayımlanan tooa kaynak grubu adında hello Pano olacaktır **panolar**. Seçin **yayımlama**.
   
     ![publish](./media/azure-portal-dashboard-share-access/publish.png)

Panonuz artık yayımlanır. Merhaba abonelikten devralınan hello izinleri uygun olup olmadığını, toodo daha fazla bir şey gerekmez. Kuruluşunuzda bulunan diğer kullanıcıların mümkün tooaccess olması ve bunların abonelik düzeyi rolüne dayalı hello Pano değiştirin. Ancak, Bu öğretici için şirketinizdeki kullanıcılar tooa rolü bu Pano için bir grup atayın.

## <a name="assign-access-tooa-dashboard"></a>Erişim tooa Panosu Ata
1. Merhaba Pano yayımlandıktan sonra Seç **kullanıcıları yönetme**.
   
     ![Kullanıcıları yönetme](./media/azure-portal-dashboard-share-access/manage-users.png)
2. Bu Pano için bir rol zaten atanmış olan kullanıcıların bir listesini görürsünüz. Mevcut kullanıcıları listenize görüntü hello aşağıdaki farklı olacaktır. Büyük olasılıkla hello atamaları hello abonelikten devralınır. tooadd yeni bir kullanıcı veya grubu seçin **Ekle**.
   
     ![Kullanıcı Ekle](./media/azure-portal-dashboard-share-access/existing-users.png)
3. Merhaba izinleri toogrant istediğiniz temsil eden hello rolü seçin. Bu örnek için select **katkıda bulunan**.
   
     ![Rol Seç](./media/azure-portal-dashboard-share-access/select-role.png)
4. Merhaba kullanıcı veya tooassign toohello rol istediğiniz grubu seçin. Merhaba kullanıcı veya grup hello listesinde aradığınız görmüyorsanız hello arama kutusunu kullanın. Kullanılabilir grupları listesi, Active Directory'de oluşturduğunuz hello gruplarında bağlıdır.
   
     ![Kullanıcı Seç](./media/azure-portal-dashboard-share-access/select-user.png) 
5. Kullanıcıları veya grupları eklemeyi tamamladığınızda seçin **Tamam**. 
6. Merhaba yeni atama kullanıcıların toohello listesini eklenir. Şunlara dikkat edin, **erişim** olarak listelenen **atanan** yerine **devralınan**.
   
     ![atanan roller](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a>Sonraki adımlar
* Rollerinin listesi için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).
* Kaynakları yönetme hakkında toolearn bkz [yönetmek Azure kaynakları portal üzerinden](resource-group-portal.md).

