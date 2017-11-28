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
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="5a25c-103">Toosecure toodata kataloğu ve veri varlıklarını nasıl erişim</span><span class="sxs-lookup"><span data-stu-id="5a25c-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5a25c-104">Bu özellik yalnızca hello standard Edition'da Azure veri Kataloğu'nun kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a25c-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="5a25c-105">Azure veri Kataloğu hello veri kataloğu ve ne erişebilen toospecify verir işlemleri (kayıt, açıklama, Sahipliği Al) hello kataloğunda meta veriler üzerinde gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a25c-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="5a25c-106">Katalog kullanıcıları ve izinleri</span><span class="sxs-lookup"><span data-stu-id="5a25c-106">Catalog users and permissions</span></span>
<span data-ttu-id="5a25c-107">toogive bir kullanıcının veya grubun hello tooa veri Kataloğu'na gidin ve izinleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="5a25c-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="5a25c-108">Merhaba üzerinde [, veri Kataloğu giriş sayfasına](http://www.azuredatacatalog.com), tıklatın **ayarları** hello araç.</span><span class="sxs-lookup"><span data-stu-id="5a25c-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![Veri Kataloğu - ayarlar](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="5a25c-110">Merhaba Hello Ayarları sayfasında genişletin **katalog kullanıcıları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="5a25c-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="5a25c-111">![Kullanıcılar - katalog ekleme](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="5a25c-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="5a25c-112">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a25c-112">Click **Add**.</span></span>
4. <span data-ttu-id="5a25c-113">Tam hello girin **kullanıcı adı** veya hello adını **güvenlik grubu** hello Azure Active Directory (AAD) hello Kataloğu ile ilişkili olarak.</span><span class="sxs-lookup"><span data-stu-id="5a25c-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="5a25c-114">Virgül kullanın (', ') ekliyorsanız ayırıcı birden fazla bir kullanıcı veya grup olarak.</span><span class="sxs-lookup"><span data-stu-id="5a25c-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="5a25c-115">![Katalog kullanıcıları - kullanıcıları veya grupları](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="5a25c-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="5a25c-116">Tuşuna **ENTER** veya **sekmesini** hello metin kutusu dışında.</span><span class="sxs-lookup"><span data-stu-id="5a25c-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="5a25c-117">Onaylayın tüm izinleri (**Açıklama Ekle**, **kaydetmek**, ve **Sahipliği Al**) toothese kullanıcıları veya grupları varsayılan olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="5a25c-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="5a25c-118">Diğer bir deyişle, hello kullanıcı veya grup için [veri varlıklarını kaydetme]( data-catalog-how-to-register.md), [veri varlıklarına açıklama]( data-catalog-how-to-annotate.md), ve [veri varlıklarının sahipliğini]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="5a25c-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="5a25c-119">![Katalog kullanıcıları - varsayılan izinleri](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="5a25c-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="5a25c-120">bir kullanıcı veya grup toogive yalnızca erişim toohello katalog hello okuma hello temizleyin **açıklama** kullanıcı veya grup için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5a25c-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="5a25c-121">Bunu yaptığınızda hello kullanıcı veya grup hello katalogdaki veri varlıklarına açıklama olamaz ancak bunları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a25c-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="5a25c-122">toodeny bir kullanıcı ya da veri varlıklarını kaydetme grubunun temizleyin hello **kaydetmek** kullanıcı veya grup için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5a25c-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="5a25c-123">bir kullanıcının bir veri varlığına Temizle hello sahipliğini toodeny **sahipliğini** seçeneği kullanıcı veya grup için.</span><span class="sxs-lookup"><span data-stu-id="5a25c-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="5a25c-124">toodelete katalog kullanıcıları, bir kullanıcıyı/grubu tıklatın **x** hello kullanıcı/Grup hello listesinin hello altındaki için.</span><span class="sxs-lookup"><span data-stu-id="5a25c-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="5a25c-125">![Kullanıcıların katalog - kullanıcı silme](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="5a25c-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5a25c-126">Kullanıcı ekleme yerine güvenlik grupları toocatalog kullanıcılar doğrudan ekleyin ve izinleri atayın öneririz.</span><span class="sxs-lookup"><span data-stu-id="5a25c-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="5a25c-127">Ardından, rollerine ve bunların gerekli erişim toohello katalog eşleşen kullanıcıları toohello güvenlik gruplarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5a25c-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="5a25c-128">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="5a25c-128">Special considerations</span></span>

- <span data-ttu-id="5a25c-129">Hello izinleri toosecurity grupları atanmış olan eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5a25c-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="5a25c-130">Örneğin, bir iki grupta kullanıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="5a25c-130">Say, a user is in two groups.</span></span> <span data-ttu-id="5a25c-131">Bir grup izinleri ek açıklama ve diğer grup değil sahip açıklama izinleri.</span><span class="sxs-lookup"><span data-stu-id="5a25c-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="5a25c-132">Ardından, kullanıcı sahip açıklama izinleri.</span><span class="sxs-lookup"><span data-stu-id="5a25c-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="5a25c-133">Merhaba izinleri açıkça atanan izinler toogroups toowhich hello kullanıcının ait olduğu tooa kullanıcı geçersiz kılma hello atanır.</span><span class="sxs-lookup"><span data-stu-id="5a25c-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="5a25c-134">Merhaba önceki örnekte söyleyin hello kullanıcı toocatalog kullanıcılar açıkça eklenen ve değil atama izinleri ek açıklama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a25c-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="5a25c-135">Merhaba kullanıcı sahip bir grup üyesi açıklama izinler olsa bile hello kullanıcı veri varlıklarına açıklama olamaz.</span><span class="sxs-lookup"><span data-stu-id="5a25c-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a25c-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5a25c-136">Next steps</span></span>
- [<span data-ttu-id="5a25c-137">Azure Veri Kataloğu ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5a25c-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

