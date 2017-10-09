---
title: "aaaAzure rol tabanlı erişim denetimi (RBAC) toocontrol erişim hakları toocreate ve Destek isteklerini yönetme | Microsoft Docs"
description: "Azure rol tabanlı erişim denetimi (RBAC) toocontrol hakları toocreate erişmek ve Destek isteklerini yönet"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a>Azure rol tabanlı erişim denetimi (RBAC) toocontrol hakları toocreate erişmek ve Destek isteklerini yönet

[Rol tabanlı erişim denetimi (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) Azure için ayrıntılı erişim yönetimi sağlar.
Hello Azure portal, isteği oluşturmayı destekleyen [portal.azure.com](https://portal.azure.com), oluşturabilen ve Destek isteklerini yönet Azure RBAC modeli toodefine kullanır.
Merhaba uygun RBAC rolü toousers, grupları ve uygulamaları bir abonelik, kaynak grubu veya bir kaynak olabilen bir kapsamda belirli, atanarak erişim verilir.

Bir örnek atalım: hello abonelik kapsamında Okuma izinlerine sahip bir kaynak grubu sahibi olarak Web siteleri, sanal makineler ve alt ağlar gibi hello kaynak grubundaki tüm hello kaynakları yönetebilir.
Ancak, toocreate bir destek isteği hello sanal makine kaynağı karşı çalıştığınızda, aşağıdaki hata hello karşılaşırsanız

![Abonelik hatası](./media/create-manage-support-requests-using-access-control/subscription-error.png)

Destek isteği Yönetimi ' nde yazma izni veya hello sahip bir rolü hello abonelik kapsam toobe mümkün toocreate Microsoft.Support/* eylemde desteklemek ve Destek isteklerini yönetin.

aşağıdaki makaleye bakın hello nasıl Azure'un özel rol tabanlı erişim denetimi (RBAC) toocreate kullanın ve Destek isteklerine hello Azure portalı Yönet açıklar.

## <a name="getting-started"></a>Başlarken

Bir özel RBAC rolü hello abonelikte hello abonelik sahibi tarafından atanmış ise yukarıdaki hello örneği kullanarak, mümkün toocreate bir destek isteği bir kaynak olabilir.
[Özel RBAC rolleri](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) Azure PowerShell, Azure komut satırı arabirimi (CLI) ve hello REST API'si kullanılarak oluşturulabilir.

özel bir rol Hello Eylemler özelliği hello Azure işlemleri toowhich hello rol erişim verir belirtir.
toocreate destek isteği yönetimi için özel bir rol, hello rolü hello eylem Microsoft.Support/* sahip olması gerekir

Toocreate kullanın ve yönetmek için özel bir rol örneği destek istekleri.
Bu rolün "Destek isteği katkıda bulunan" adlı ve nasıl Biz bu makalede özel rol toohello bakın.

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

Özetlenen hello adımları [bu videoyu](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn nasıl toocreate aboneliğiniz için özel bir rol.

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a>Oluşturma ve Destek isteklerine hello Azure portalı Yönet

Bir örnek atalım – abonelik "Visual Studio MSDN aboneliğiniz." Merhaba sahibi olan
Joe kimin kaynak sahibi toosome bu Abonelikteki hello kaynak gruplarının olduğunu ve izin toohello abonelik okuma, eş ' dir.
Toogive erişim tooyour eş, Can, hello özelliği toocreate istiyor ve bu abonelik altında hello kaynaklar için destek biletlerini yönetme.

1. Merhaba ilk toogo toohello abonelik adımdır ve "Ayarlar" altında kullanıcıların bir listesini görürsünüz. Merhaba kullanıcı abonelik hello üzerinde okuyucu erişimi olan Can'i tıklatın ve şimdi yeni bir özel rol toohim atayın.

    ![Rol Ekle](./media/create-manage-support-requests-using-access-control/add-role.png)

2. "Ekle" hello "Kullanıcılar" dikey altında tıklayın. Merhaba özel rol "Destek isteği katkıda bulunan" Merhaba rollerinin listesinden seçin

    ![Destek katkıda bulunan rolü Ekle](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. Merhaba rol adı seçtikten sonra "Kullanıcı Ekle" yi tıklatın ve hello Can'ın e-posta kimlik bilgilerini girin. "Seç"'i tıklatın

    ![Kullanıcı ekle](./media/create-manage-support-requests-using-access-control/add-users.png)

4. "Tamam" tooproceed tıklatın

    ![Erişim Ekle](./media/create-manage-support-requests-using-access-control/add-access.png)

5. Şimdi hello yeni eklenen özel rol "Destek isteği katkıda bulunan" Merhaba sahibi olduğunuz hello abonelik altında hello kullanıcıyla bakın

    ![Eklenen kullanıcı](./media/create-manage-support-requests-using-access-control/user-added.png)

    Joe hello Portalı'nda oturum açtığında, kendisinin eklendi hello abonelik toowhich görür.

7. Joe "Yeni destek isteği" hello "Yardım ve desteği" dikey penceresinden tıklar ve "Visual Studio Ultimate ile MSDN için" destek istekleri oluşturabilirsiniz

    ![Yeni destek isteği](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. "Tüm istekleri desteği" tıklatarak CAN Bu abonelik için oluşturduğunuz destek isteklerini hello listesini görebilir ![durum görünümü ayrıntıları](./media/create-manage-support-requests-using-access-control/case-details-view.png)

## <a name="remove-support-request-access-in-hello-azure-portal"></a>Destek isteği erişim hello Azure portal Kaldır

Yalnızca bu olası toogrant erişim tooa kullanıcı toocreate ve Destek isteklerini yönetme gibi olası tooremove erişim hello kullanıcı için gereklidir.
tooremove özelliği toocreate hello ve Destek isteklerini yönetin, toohello abonelik gidin, "Ayarlar"'ı tıklatın ve hello kullanıcıya (Bu örnekte, Can) tıklatın.
Merhaba rol adı, "Destek isteği katkıda bulunan" sağ tıklatın ve "Kaldır"

![Destek isteği erişimi Kaldır](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

Joe toohello Portalı'nda günlüğe kaydeder ve toocreate bir destek isteği çalışırsa, kendisinin aşağıdaki hata hello karşılaştığında

![Abonelik hata-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

Joe herhangi göremezsiniz "Tüm istekleri desteği" tıklatır dağıtırken istekleri desteği

![Servis Talebi Ayrıntıları görünümü-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
