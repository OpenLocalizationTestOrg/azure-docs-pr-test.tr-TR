---
title: "aaaHow toosecure erişim tooAzure veri Kataloğu | Microsoft Docs"
description: "Bu makalede açıklayan nasıl toosecure veri kataloğu ve veri varlıklarını."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Toosecure toodata kataloğu ve veri varlıklarını nasıl erişim
> [!IMPORTANT]
> Bu özellik yalnızca hello standard Edition'da Azure veri Kataloğu'nun kullanılabilir.

Azure veri Kataloğu hello veri kataloğu ve ne erişebilen toospecify verir işlemleri (kayıt, açıklama, Sahipliği Al) hello kataloğunda meta veriler üzerinde gerçekleştirebilirsiniz. 

## <a name="catalog-users-and-permissions"></a>Katalog kullanıcıları ve izinleri
toogive bir kullanıcının veya grubun hello tooa veri Kataloğu'na gidin ve izinleri ayarlayın:

1. Merhaba üzerinde [, veri Kataloğu giriş sayfasına](http://www.azuredatacatalog.com), tıklatın **ayarları** hello araç.

    ![Veri Kataloğu - ayarlar](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. Merhaba Hello Ayarları sayfasında genişletin **katalog kullanıcıları** bölümü.
    ![Kullanıcılar - katalog ekleme](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. **Ekle**'ye tıklayın.
4. Tam hello girin **kullanıcı adı** veya hello adını **güvenlik grubu** hello Azure Active Directory (AAD) hello Kataloğu ile ilişkili olarak. Virgül kullanın (', ') ekliyorsanız ayırıcı birden fazla bir kullanıcı veya grup olarak.
    ![Katalog kullanıcıları - kullanıcıları veya grupları](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. Tuşuna **ENTER** veya **sekmesini** hello metin kutusu dışında. 
6.  Onaylayın tüm izinleri (**Açıklama Ekle**, **kaydetmek**, ve **Sahipliği Al**) toothese kullanıcıları veya grupları varsayılan olarak atanır. Diğer bir deyişle, hello kullanıcı veya grup için [veri varlıklarını kaydetme]( data-catalog-how-to-register.md), [veri varlıklarına açıklama]( data-catalog-how-to-annotate.md), ve [veri varlıklarının sahipliğini]( data-catalog-how-to-manage.md). 
    ![Katalog kullanıcıları - varsayılan izinleri](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  bir kullanıcı veya grup toogive yalnızca erişim toohello katalog hello okuma hello temizleyin **açıklama** kullanıcı veya grup için seçeneği. Bunu yaptığınızda hello kullanıcı veya grup hello katalogdaki veri varlıklarına açıklama olamaz ancak bunları görüntüleyebilirsiniz. 
8.  toodeny bir kullanıcı ya da veri varlıklarını kaydetme grubunun temizleyin hello **kaydetmek** kullanıcı veya grup için seçeneği.
9.  bir kullanıcının bir veri varlığına Temizle hello sahipliğini toodeny **sahipliğini** seçeneği kullanıcı veya grup için. 
10. toodelete katalog kullanıcıları, bir kullanıcıyı/grubu tıklatın **x** hello kullanıcı/Grup hello listesinin hello altındaki için. 
    ![Kullanıcıların katalog - kullanıcı silme](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > Kullanıcı ekleme yerine güvenlik grupları toocatalog kullanıcılar doğrudan ekleyin ve izinleri atayın öneririz. Ardından, rollerine ve bunların gerekli erişim toohello katalog eşleşen kullanıcıları toohello güvenlik gruplarını ekleyin.

## <a name="special-considerations"></a>Özel durumlar

- Hello izinleri toosecurity grupları atanmış olan eklenebilir. Örneğin, bir iki grupta kullanıcısıdır. Bir grup izinleri ek açıklama ve diğer grup değil sahip açıklama izinleri. Ardından, kullanıcı sahip açıklama izinleri. 
- Merhaba izinleri açıkça atanan izinler toogroups toowhich hello kullanıcının ait olduğu tooa kullanıcı geçersiz kılma hello atanır. Merhaba önceki örnekte söyleyin hello kullanıcı toocatalog kullanıcılar açıkça eklenen ve değil atama izinleri ek açıklama ekleyebilirsiniz. Merhaba kullanıcı sahip bir grup üyesi açıklama izinler olsa bile hello kullanıcı veri varlıklarına açıklama olamaz.

## <a name="next-steps"></a>Sonraki adımlar
- [Azure Veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md)

