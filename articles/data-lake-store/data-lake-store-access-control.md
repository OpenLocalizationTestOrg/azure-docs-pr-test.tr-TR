---
title: "erişim denetimi Data Lake Store'da aaaOverview | Microsoft Docs"
description: "Azure Data Lake Store’da erişim denetiminin çalışma şekli hakkında bilgi edinin"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="3a9d1-103">Azure Data Lake Store’da erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="3a9d1-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="3a9d1-104">Azure Data Lake Store sırayla hello POSIX erişim denetimi modeli türetilen HDFS türeyen bir erişim denetimi modeli uygular.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="3a9d1-105">Bu makalede hello erişim denetimi modeli Data Lake Store için hello temelleri özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="3a9d1-106">toolearn hello HDFS erişim denetimi modeli hakkında daha fazla bilgi görmek [HDFS izinleri Kılavuzu](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="3a9d1-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="3a9d1-107">Dosyalar ve klasörler üzerindeki erişim denetimi listeleri</span><span class="sxs-lookup"><span data-stu-id="3a9d1-107">Access control lists on files and folders</span></span>

<span data-ttu-id="3a9d1-108">İki tür erişim denetim listesi (ACL) vardır: **Erişim ACL’leri** ve **Varsayılan ACL’ler**.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="3a9d1-109">**Erişim ACL'ler**: Bu denetim erişim tooan nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="3a9d1-110">Hem dosyalar hem de klasörler Erişim ACL’lerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="3a9d1-111">**Varsayılan ACL'leri**: "Bu klasörü altında oluşturulan tüm alt öğeleri için hello erişim ACL'ler belirleyen bir klasörle ilişkili şablonu" ACL'leri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="3a9d1-112">Dosyalar Varsayılan ACL’ye sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-112">Files do not have Default ACLs.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="3a9d1-114">Erişim ACL'ler ve varsayılan ACL'leri sahip hello aynı yapısı.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="3a9d1-116">Bir üst hello varsayılan ACL değişen hello erişim ACL veya varsayılan ACL zaten alt öğelerinin etkilemez.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="3a9d1-117">Kullanıcılar ve kimlikler</span><span class="sxs-lookup"><span data-stu-id="3a9d1-117">Users and identities</span></span>

<span data-ttu-id="3a9d1-118">Her dosya ve klasör bu kimlikler için farklı izinlere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3a9d1-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="3a9d1-119">sahibi olan kullanıcı hello dosyasının hello</span><span class="sxs-lookup"><span data-stu-id="3a9d1-119">hello owning user of hello file</span></span>
* <span data-ttu-id="3a9d1-120">Merhaba sahibi olan Grup</span><span class="sxs-lookup"><span data-stu-id="3a9d1-120">hello owning group</span></span>
* <span data-ttu-id="3a9d1-121">Adlandırılmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="3a9d1-121">Named users</span></span>
* <span data-ttu-id="3a9d1-122">Adlandırılmış gruplar</span><span class="sxs-lookup"><span data-stu-id="3a9d1-122">Named groups</span></span>
* <span data-ttu-id="3a9d1-123">Diğer tüm kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="3a9d1-123">All other users</span></span>

<span data-ttu-id="3a9d1-124">Merhaba kimlikleri kullanıcıların ve grupların Azure Active Directory (Azure AD) hesaplardır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="3a9d1-125">Aksi belirtilmediği sürece, bir "kullanıcı" Merhaba bağlamındaki Data Lake Store, bu nedenle herhangi bir Azure AD kullanıcısının veya bir Azure AD güvenlik grubuna anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="3a9d1-126">İzinler</span><span class="sxs-lookup"><span data-stu-id="3a9d1-126">Permissions</span></span>

<span data-ttu-id="3a9d1-127">bir dosya sistemi nesnenin Hello izinleri olan **okuma**, **yazma**, ve **yürütme**, ve dosya ve klasörleri aşağıdaki tablonun hello gösterildiği gibi kullanılabilmesi için:</span><span class="sxs-lookup"><span data-stu-id="3a9d1-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="3a9d1-128">Dosya</span><span class="sxs-lookup"><span data-stu-id="3a9d1-128">File</span></span>     |   <span data-ttu-id="3a9d1-129">Klasör</span><span class="sxs-lookup"><span data-stu-id="3a9d1-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="3a9d1-130">**Okuma (R)**</span><span class="sxs-lookup"><span data-stu-id="3a9d1-130">**Read (R)**</span></span> | <span data-ttu-id="3a9d1-131">Bir dosyanın içeriğini Hello okuyabilir</span><span class="sxs-lookup"><span data-stu-id="3a9d1-131">Can read hello contents of a file</span></span> | <span data-ttu-id="3a9d1-132">Gerektirir **okuma** ve **yürütme** toolist hello hello klasörünün içeriğini</span><span class="sxs-lookup"><span data-stu-id="3a9d1-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="3a9d1-133">**Yazma (W)**</span><span class="sxs-lookup"><span data-stu-id="3a9d1-133">**Write (W)**</span></span> | <span data-ttu-id="3a9d1-134">Yazma veya tooa dosya ekleme</span><span class="sxs-lookup"><span data-stu-id="3a9d1-134">Can write or append tooa file</span></span> | <span data-ttu-id="3a9d1-135">Gerektirir **yazma** ve **yürütme** klasöründeki toocreate alt öğeleri</span><span class="sxs-lookup"><span data-stu-id="3a9d1-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="3a9d1-136">**Yürütme (X)**</span><span class="sxs-lookup"><span data-stu-id="3a9d1-136">**Execute (X)**</span></span> | <span data-ttu-id="3a9d1-137">Data Lake Store hello bağlamında herhangi bir şey gelmez</span><span class="sxs-lookup"><span data-stu-id="3a9d1-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="3a9d1-138">Bir klasörün gerekli tootraverse hello alt öğeleri</span><span class="sxs-lookup"><span data-stu-id="3a9d1-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="3a9d1-139">İzinlerin kısaltmaları</span><span class="sxs-lookup"><span data-stu-id="3a9d1-139">Short forms for permissions</span></span>

<span data-ttu-id="3a9d1-140">**RWX** kullanılan tooindicate olan **okuma + yazma + yürütme**.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="3a9d1-141">Daha fazla sıkıştırılmış bir sayısal form bulunduğu **okuma = 4**, **yazma = 2**, ve **Execute = 1**, hangi hello toplamını hello izinleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="3a9d1-142">Bazı örnekler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-142">Following are some examples.</span></span>

| <span data-ttu-id="3a9d1-143">Sayısal biçim</span><span class="sxs-lookup"><span data-stu-id="3a9d1-143">Numeric form</span></span> | <span data-ttu-id="3a9d1-144">Kısa biçim</span><span class="sxs-lookup"><span data-stu-id="3a9d1-144">Short form</span></span> |      <span data-ttu-id="3a9d1-145">Anlamı</span><span class="sxs-lookup"><span data-stu-id="3a9d1-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="3a9d1-146">7</span><span class="sxs-lookup"><span data-stu-id="3a9d1-146">7</span></span>            | <span data-ttu-id="3a9d1-147">RWX</span><span class="sxs-lookup"><span data-stu-id="3a9d1-147">RWX</span></span>        | <span data-ttu-id="3a9d1-148">Okuma + Yazma + Yürütme</span><span class="sxs-lookup"><span data-stu-id="3a9d1-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="3a9d1-149">5</span><span class="sxs-lookup"><span data-stu-id="3a9d1-149">5</span></span>            | <span data-ttu-id="3a9d1-150">R-X</span><span class="sxs-lookup"><span data-stu-id="3a9d1-150">R-X</span></span>        | <span data-ttu-id="3a9d1-151">Okuma + Yürütme</span><span class="sxs-lookup"><span data-stu-id="3a9d1-151">Read + Execute</span></span>         |
| <span data-ttu-id="3a9d1-152">4</span><span class="sxs-lookup"><span data-stu-id="3a9d1-152">4</span></span>            | <span data-ttu-id="3a9d1-153">R--</span><span class="sxs-lookup"><span data-stu-id="3a9d1-153">R--</span></span>        | <span data-ttu-id="3a9d1-154">Okuma</span><span class="sxs-lookup"><span data-stu-id="3a9d1-154">Read</span></span>                   |
| <span data-ttu-id="3a9d1-155">0</span><span class="sxs-lookup"><span data-stu-id="3a9d1-155">0</span></span>            | ---        | <span data-ttu-id="3a9d1-156">İzin yok</span><span class="sxs-lookup"><span data-stu-id="3a9d1-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="3a9d1-157">İzinler devralınmaz</span><span class="sxs-lookup"><span data-stu-id="3a9d1-157">Permissions do not inherit</span></span>

<span data-ttu-id="3a9d1-158">Data Lake Store tarafından kullanılan hello POSIX tipi modelinde, bir öğe için izinleri hello öğede depolanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="3a9d1-159">Diğer bir deyişle, bir öğe için izinleri hello üst öğelerinden devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="3a9d1-160">Yaygın senaryolar ilgili toopermissions</span><span class="sxs-lookup"><span data-stu-id="3a9d1-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="3a9d1-161">Şunlardır anlamak hangi izinlerin olduğunu bazı ortak senaryolar toohelp belirli işlemlerin bir Data Lake Store hesabındaki tooperform gerekli.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="3a9d1-162">Bir dosya tooread gereken izinler</span><span class="sxs-lookup"><span data-stu-id="3a9d1-162">Permissions needed tooread a file</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="3a9d1-164">Okuma hello dosya toobe için hello çağıran gereksinimlerini **okuma** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="3a9d1-165">Tüm hello dosyasını içeren hello Klasör yapısındaki klasörler hello için hello çağıran gereksinimlerini **yürütme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="3a9d1-166">Tooappend tooa dosya gereken izinler</span><span class="sxs-lookup"><span data-stu-id="3a9d1-166">Permissions needed tooappend tooa file</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="3a9d1-168">Merhaba dosya toobe eklenen için hello çağıran gereksinimlerini **yazma** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="3a9d1-169">Tüm hello dosya içeren klasörleri hello için hello çağıran gereksinimlerini **yürütme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="3a9d1-170">Bir dosya toodelete gereken izinler</span><span class="sxs-lookup"><span data-stu-id="3a9d1-170">Permissions needed toodelete a file</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="3a9d1-172">Merhaba üst klasör için hello çağıran gereksinimlerini **yazma + yürütme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="3a9d1-173">Tüm diğer hello dosyanın yolu klasörlerde hello için hello çağıran gereksinimlerini **yürütme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="3a9d1-174">Merhaba dosyanın izinlerini önceki iki koşul hello sürece bunu true gerekli toodelete olmayan yazma.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="3a9d1-175">Bir klasör tooenumerate gereken izinler</span><span class="sxs-lookup"><span data-stu-id="3a9d1-175">Permissions needed tooenumerate a folder</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="3a9d1-177">Başlangıç klasörü tooenumerate için hello çağıran gereksinimlerini **okuma + yürütme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="3a9d1-178">Tüm üst klasörlerin hello için hello çağıran gereksinimlerini **yürütme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="3a9d1-179">Hello Azure portalı izinlerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="3a9d1-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="3a9d1-180">Merhaba gelen **Veri Gezgini** hello Data Lake Store hesabı dikey tıklayın **erişim** toosee hello ACL'ler bir dosya veya klasör.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="3a9d1-181">Tıklatın **erişim** toosee Merhaba ACL'ler hello **katalog** hello altında bir klasör **mydatastore** hesabı.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="3a9d1-183">Bu dikey penceresinde hello üst kısmında elinizde hello izinleri genel bir bakış gösterilir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="3a9d1-184">(Merhaba ekran görüntüsünde, hello Bob kullanıcıdır.) Hello erişim izinleri gösterilir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="3a9d1-185">Bundan sonra gelen hello **erişim** dikey penceresinde tıklatın **Basit Görünüm** toosee hello daha basit görünümü.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="3a9d1-187">Tıklatın **Gelişmiş Görünüm** Gelişmiş daha görünümü toosee hello varsayılan ACL'leri, maskesi ve süper kullanıcı hello kavramlarını burada gösterilir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="3a9d1-189">Merhaba süper kullanıcı</span><span class="sxs-lookup"><span data-stu-id="3a9d1-189">hello super-user</span></span>

<span data-ttu-id="3a9d1-190">Süper kullanıcı hello hello Data Lake Store tüm hello kullanıcıların çoğu haklara sahip olur.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="3a9d1-191">Süper kullanıcı:</span><span class="sxs-lookup"><span data-stu-id="3a9d1-191">A super-user:</span></span>

* <span data-ttu-id="3a9d1-192">Çok RWX izinlerine sahip**tüm** dosyalar ve klasörler.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="3a9d1-193">Herhangi bir dosya veya klasör Hello izinleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="3a9d1-194">Sahibi olan kullanıcı veya grubu herhangi bir dosya veya klasör hello değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="3a9d1-195">Azure’da bir Data Lake Store hesabının birkaç Azure rolü vardır, bunlar:</span><span class="sxs-lookup"><span data-stu-id="3a9d1-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="3a9d1-196">Sahipler</span><span class="sxs-lookup"><span data-stu-id="3a9d1-196">Owners</span></span>
* <span data-ttu-id="3a9d1-197">Katkıda Bulunanlar</span><span class="sxs-lookup"><span data-stu-id="3a9d1-197">Contributors</span></span>
* <span data-ttu-id="3a9d1-198">Okuyucular</span><span class="sxs-lookup"><span data-stu-id="3a9d1-198">Readers</span></span>

<span data-ttu-id="3a9d1-199">Herkesin hello **sahipleri** bir Data Lake Store hesabı rolüdür otomatik olarak bu hesap için süper kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="3a9d1-200">toolearn daha, fazla [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3a9d1-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="3a9d1-201">Toocreate süper kullanıcı izinlerine sahip bir özel rol tabanlı erişim denetimi (RBAC) rolüne istiyorsanız, aşağıdaki izinleri toohave hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3a9d1-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="3a9d1-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="3a9d1-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="3a9d1-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="3a9d1-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="3a9d1-204">Merhaba sahibi olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="3a9d1-204">hello owning user</span></span>

<span data-ttu-id="3a9d1-205">Merhaba öğesini oluşturan hello otomatik olarak kullanıcı hello öğesinin sahibi olan hello kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="3a9d1-206">Sahip olan kullanıcı şunları yapabilir:</span><span class="sxs-lookup"><span data-stu-id="3a9d1-206">An owning user can:</span></span>

* <span data-ttu-id="3a9d1-207">Ait bir dosyanın Hello izinleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="3a9d1-208">Merhaba sahibi olan kullanıcı da hello hedef grubunun bir üyesi olduğu sürece aitse, bir dosya grubunun sahibi olan hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="3a9d1-209">sahibi olan kullanıcı hello *olamaz* sahibi olan kullanıcı başka bir ait dosyasının hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="3a9d1-210">Yalnızca süper kullanıcılar, kullanıcı bir dosyanın veya klasörün sahibi olan hello değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="3a9d1-211">Merhaba sahibi olan Grup</span><span class="sxs-lookup"><span data-stu-id="3a9d1-211">hello owning group</span></span>

<span data-ttu-id="3a9d1-212">Hello POSIX ACL'leri, her kullanıcı bir "birincil grubuyla." ilişkilendirildiği</span><span class="sxs-lookup"><span data-stu-id="3a9d1-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="3a9d1-213">Örneğin, kullanıcı "alice" toohello "Finans" grubuna ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="3a9d1-214">Alice toomultiple grupları ait olabilir, ancak bir grup her zaman kendi birincil grup olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="3a9d1-215">Bir dosya Alice oluşturduğunda, POSIX içinde bu durumda "Finans.", tooher birincil grubu bu dosya grubu hello ayarlanmış</span><span class="sxs-lookup"><span data-stu-id="3a9d1-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="3a9d1-216">Yeni bir dosya sistemi öğesi oluşturulduğunda, Data Lake Store Grup sahibi olan bir değer toohello atar.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="3a9d1-217">**Durum 1**: hello kök klasörü "/".</span><span class="sxs-lookup"><span data-stu-id="3a9d1-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="3a9d1-218">Bir Data Lake Store hesabı oluşturulduğunda bu klasör oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="3a9d1-219">Bu durumda, hello sahibi olan Grup hello hesap oluşturan toohello kullanıcı ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="3a9d1-220">**Durum 2** (her diğer harf): yeni bir öğe oluşturulduğunda hello sahibi olan Grup hello üst klasörden kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="3a9d1-221">Hello sahibi olan grup tarafından değiştirilebilen:</span><span class="sxs-lookup"><span data-stu-id="3a9d1-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="3a9d1-222">Herhangi bir süper kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-222">Any super-users.</span></span>
* <span data-ttu-id="3a9d1-223">Merhaba Hello sahibi olan kullanıcı aynı zamanda hello hedef grubunun bir üyesi ise kullanıcı yapamaz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="3a9d1-224">Erişim denetimi algoritması</span><span class="sxs-lookup"><span data-stu-id="3a9d1-224">Access check algorithm</span></span>

<span data-ttu-id="3a9d1-225">Aşağıdaki çizimde hello hello erişim denetimi algoritması için Data Lake Store hesaplarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Data Lake Store ACL’leri algoritması](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="3a9d1-227">Merhaba maskesi ve "etkili izinleri"</span><span class="sxs-lookup"><span data-stu-id="3a9d1-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="3a9d1-228">Merhaba **maskesi** bir RWX olan değer için kullanılan toolimit erişim **kullanıcı adlı**, hello **grubu**, ve **grupları adlı** olduğunuzda Merhaba erişim denetimi algoritması gerçekleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="3a9d1-229">Merhaba hello maskesi için temel kavramları şunlardır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="3a9d1-230">"yürürlükte olan izinlerini." Merhaba maskesi oluşturur</span><span class="sxs-lookup"><span data-stu-id="3a9d1-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="3a9d1-231">Diğer bir deyişle, erişim denetimi hello aynı anda hello izinlerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="3a9d1-232">Merhaba maskesi doğrudan hello dosya sahibine ve Süper kullanıcılar tarafından düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="3a9d1-233">Merhaba maskesi izinleri toocreate hello etkili izni kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="3a9d1-234">Merhaba maskesi *olamaz* izinleri toohello etkili izni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="3a9d1-235">Bazı örneklere bakalım.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-235">Let's look at some examples.</span></span> <span data-ttu-id="3a9d1-236">Aşağıdaki örneğine hello hello maskesi çok ayarlanır**RWX**, o hello maskesi başka bir deyişle, tüm izinleri kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="3a9d1-237">Merhaba adlı grubu ve grubun adlı kullanıcının hello yürürlükte olan izinlerini hello erişim denetimi sırasında değiştirilmediğini değil.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="3a9d1-239">Aşağıdaki örneğine hello hello maskesi çok ayarlanır**R-X**.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="3a9d1-240">Bu şekilde gelir **hello yazma izinleri devre dışı bırakır** için **adlı kullanıcının**, **grubu**, ve **Grup adlı** hello zaman erişim denetleyin.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="3a9d1-242">Başvuru için İşte bir dosya veya klasör için hello maskesi hello Azure portalında göründüğü.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="3a9d1-244">Yeni bir Data Lake Store hesabı, hello erişim ACL hello maskesini ve varsayılan ACL hello kök için tooRWX klasörü ("/") varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="3a9d1-245">Yeni dosyalar ve klasörler üzerindeki izinler</span><span class="sxs-lookup"><span data-stu-id="3a9d1-245">Permissions on new files and folders</span></span>

<span data-ttu-id="3a9d1-246">Yeni bir dosya veya klasörün altında varolan bir klasörü oluşturulduğunda hello hello üst klasörü üzerinde ACL varsayılan belirler:</span><span class="sxs-lookup"><span data-stu-id="3a9d1-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="3a9d1-247">Bir alt klasörün Varsayılan ACL’si ve Erişim ACL’si.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="3a9d1-248">Bir alt dosyanın Erişim ACL’si (dosyaları Varsayılan ACL’ye sahip değildir).</span><span class="sxs-lookup"><span data-stu-id="3a9d1-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="3a9d1-249">Merhaba bir alt dosya veya klasöre erişim ACL</span><span class="sxs-lookup"><span data-stu-id="3a9d1-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="3a9d1-250">Bir alt dosya veya klasör oluşturulduğunda, hello üst öğenin varsayılan ACL hello alt dosya veya klasör erişim ACL hello kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="3a9d1-251">Ayrıca, varsa **diğer** kullanıcı hello üst öğenin varsayılan ACL RWX izinlere sahip, hello alt öğesi'nin erişim ACL'den kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="3a9d1-253">Çoğu senaryoda, hello önceki tüm alt öğenin erişim ACL belirleme hakkında tooknow ihtiyacınız bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="3a9d1-254">POSIX sistemleri ve istediğiniz toounderstand ayrıntılı bu dönüşüm nasıl gerçekleştirilir bilginiz varsa, ancak hello bölümüne bakın [yeni dosyalar ve klasörler için erişim ACL hello oluşturma Umask'ın rol](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) bu makalenin ilerisinde yer.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="3a9d1-255">Bir alt klasörün Varsayılan ACL’si</span><span class="sxs-lookup"><span data-stu-id="3a9d1-255">A child folder's Default ACL</span></span>

<span data-ttu-id="3a9d1-256">Üst klasörü altında bir alt klasör oluşturulduğunda, toohello alt klasörün varsayılan ACL olduğu gibi hello üst klasörün varsayılan ACL üzerinden kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="3a9d1-258">Data Lake Store’da ACL’leri anlamaya yönelik gelişmiş konular</span><span class="sxs-lookup"><span data-stu-id="3a9d1-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="3a9d1-259">Data Lake Store dosya ve klasörler için ACL'ler nasıl belirlendiğini anlamak bazı gelişmiş konular toohelp aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="3a9d1-260">Umask'ın rol hello erişim ACL yeni dosyalar ve klasörler için oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a9d1-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="3a9d1-261">POSIX uyumlu bir sistemde hello genel kavram, umask tootransform hello izni için kullandığı hello üst klasörde 9-bitlik bir değer olup **sahibi olan kullanıcı**, **grubu**, ve  **diğer** hello erişim ACL yeni alt dosya veya klasör üzerinde.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="3a9d1-262">bir umask Hello bitleri hangi BITS tooturn hello alt öğesi'nin erişim ACL'de kapalı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="3a9d1-263">Bu nedenle kullanılır tooselectively önlemek için izinleri hello yayılmasını **sahibi olan kullanıcı**, **grubu**, ve **diğer**.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="3a9d1-264">Bir HDFS sisteminde hello umask genellikle yöneticiler tarafından denetlenen bir sitewide yapılandırma seçenektir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="3a9d1-265">Data Lake Store değiştirilemeyen bir **hesap genelinde umask** kullanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="3a9d1-266">Aşağıdaki tablo gösterir hello hello için Data Lake Store maskesini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="3a9d1-267">Kullanıcı grubu</span><span class="sxs-lookup"><span data-stu-id="3a9d1-267">User group</span></span>  | <span data-ttu-id="3a9d1-268">Ayar</span><span class="sxs-lookup"><span data-stu-id="3a9d1-268">Setting</span></span> | <span data-ttu-id="3a9d1-269">Yeni alt öğenin Erişim ACL’si üzerindeki etkisi</span><span class="sxs-lookup"><span data-stu-id="3a9d1-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="3a9d1-270">Sahip olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="3a9d1-270">Owning user</span></span> | ---     | <span data-ttu-id="3a9d1-271">Etki yok</span><span class="sxs-lookup"><span data-stu-id="3a9d1-271">No effect</span></span>                             |
| <span data-ttu-id="3a9d1-272">Sahip olan grup</span><span class="sxs-lookup"><span data-stu-id="3a9d1-272">Owning group</span></span>| ---     | <span data-ttu-id="3a9d1-273">Etki yok</span><span class="sxs-lookup"><span data-stu-id="3a9d1-273">No effect</span></span>                             |
| <span data-ttu-id="3a9d1-274">Diğer</span><span class="sxs-lookup"><span data-stu-id="3a9d1-274">Other</span></span>       | <span data-ttu-id="3a9d1-275">RWX</span><span class="sxs-lookup"><span data-stu-id="3a9d1-275">RWX</span></span>     | <span data-ttu-id="3a9d1-276">Okuma + Yazma + Yürütme iznini kaldırma</span><span class="sxs-lookup"><span data-stu-id="3a9d1-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="3a9d1-277">Aşağıdaki çizimde hello bu umask eylemde gösterir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="3a9d1-278">Merhaba net etkisidir tooremove **okuma + yazma + yürütme** için **diğer** kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="3a9d1-279">Merhaba umask BITS belirtmediğinden **sahibi olan kullanıcı** ve **grubu**, bu izinleri olmayan dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="3a9d1-281">Merhaba Yapışkan bit</span><span class="sxs-lookup"><span data-stu-id="3a9d1-281">hello sticky bit</span></span>

<span data-ttu-id="3a9d1-282">Merhaba Yapışkan bit POSIX dosya sistemi, daha gelişmiş bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="3a9d1-283">Data Lake Store Hello bağlamında bu hello Yapışkan bit gerekli düşüktür.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="3a9d1-284">Merhaba aşağıdaki tabloda hello Yapışkan bit Data Lake Store içinde nasıl çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="3a9d1-285">Kullanıcı grubu</span><span class="sxs-lookup"><span data-stu-id="3a9d1-285">User group</span></span>         | <span data-ttu-id="3a9d1-286">Dosya</span><span class="sxs-lookup"><span data-stu-id="3a9d1-286">File</span></span>    | <span data-ttu-id="3a9d1-287">Klasör</span><span class="sxs-lookup"><span data-stu-id="3a9d1-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="3a9d1-288">Yapışkan bit **Kapalı**</span><span class="sxs-lookup"><span data-stu-id="3a9d1-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="3a9d1-289">Etki yok</span><span class="sxs-lookup"><span data-stu-id="3a9d1-289">No effect</span></span>   | <span data-ttu-id="3a9d1-290">Etki yok.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-290">No effect.</span></span>           |
| <span data-ttu-id="3a9d1-291">Yapışkan bit **Açık**</span><span class="sxs-lookup"><span data-stu-id="3a9d1-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="3a9d1-292">Etki yok</span><span class="sxs-lookup"><span data-stu-id="3a9d1-292">No effect</span></span>   | <span data-ttu-id="3a9d1-293">Herkes dışında engeller **Süper kullanıcılar** ve hello **sahibi olan kullanıcı** bir alt öğenin silmesini ve o alt öğesi yeniden adlandırılıyor.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="3a9d1-294">Merhaba Yapışkan bit hello Azure portalında gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="3a9d1-295">Data Lake Store’daki ACL’ler hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="3a9d1-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="3a9d1-296">Data Lake Store’daki ACL’lerle ilgili olarak sık sorulan bazı sorular aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="3a9d1-297">ACL tooenable desteği var mı?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="3a9d1-298">Hayır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-298">No.</span></span> <span data-ttu-id="3a9d1-299">ACL’ler üzerinden erişim denetimi Data Lake Store hesabı için her zaman açıktır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="3a9d1-300">Hangi izinlerin gerekli toorecursively delete klasörü ve içeriği misiniz?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="3a9d1-301">Merhaba üst klasörü olmalıdır **yazma + yürütme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="3a9d1-302">Silinen klasör toobe hello ve her bir klasörde gerektirir **okuma + yazma + yürütme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="3a9d1-303">Klasörlerde toodelete dosyaları yazma izinleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="3a9d1-304">Ayrıca, hello kök klasörü "/" için **hiçbir zaman** silinecektir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="3a9d1-305">Bir dosya veya klasör hello sahibi kim?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="3a9d1-306">bir dosya veya klasör Hello oluşturan hello sahibi olur.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="3a9d1-307">Hangi Grup, bir dosyanın veya klasörün oluşturmada grubu hello olarak ayarlanır?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="3a9d1-308">Merhaba sahibi olan Grup hello üst klasörünün altında hangi hello yeni dosya veya klasör oluşturulur grubu hello kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="3a9d1-309">Sahibi olan kullanıcı dosyasının hello ben ama ihtiyacım hello RWX izinleri yok.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="3a9d1-310">Ne yapmalıyım?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-310">What do I do?</span></span>

<span data-ttu-id="3a9d1-311">Merhaba sahibi olan kullanıcı hello dosya toogive hello izinlerini kendilerini ihtiyaç duydukları tüm RWX izinleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="3a9d1-312">ACL'ler baktığınızda hello Azure portalı kullanıcı adları görüyorum ancak GUID, görüyorum API'leri aracılığıyla neden?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="3a9d1-313">Merhaba ACL girişleri toousers Azure AD içinde karşılık gelen GUID olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="3a9d1-314">Merhaba API'leri olduğu gibi hello GUID'ler döndür.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="3a9d1-315">Hello Azure portal toomake ACL'ler daha kolay toouse kolay adlar mümkün olduğunda içine çevirme hello GUID'ler ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="3a9d1-316">Hello Azure portalı kullanırken neden bazen hello ACL'lerinde GUID'ler görüyorum?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="3a9d1-317">Merhaba kullanıcı artık Azure AD'de mevcut olmayan bir GUID gösterilir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="3a9d1-318">Genellikle bu hello kullanıcı hello şirket bırakıldığına veya hesaplarında Azure AD'de silinmiş olması durumunda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="3a9d1-319">Data Lake Store ACL’lerin devralınmasını destekler mi?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="3a9d1-320">Hayır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="3a9d1-321">Merhaba maskesi ve umask arasındaki fark nedir?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="3a9d1-322">maske</span><span class="sxs-lookup"><span data-stu-id="3a9d1-322">mask</span></span> | <span data-ttu-id="3a9d1-323">umask</span><span class="sxs-lookup"><span data-stu-id="3a9d1-323">umask</span></span>|
|------|------|
| <span data-ttu-id="3a9d1-324">Merhaba **maskesi** özelliği, her dosya ve klasör kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="3a9d1-325">Merhaba **umask** hello Data Lake Store hesabı bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="3a9d1-326">Bu nedenle hello Data Lake Store yalnızca tek bir umask yoktur.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="3a9d1-327">bir dosya veya klasör Hello maskesi özelliği sahibi olan kullanıcı veya bir dosya veya süper kullanıcı grubu hello tarafından değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="3a9d1-328">herhangi bir kullanıcı tarafından bile süper kullanıcı Hello umask özelliği değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="3a9d1-329">Bu özellik, değiştirilemeyen sabit bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="3a9d1-330">bir kullanıcı işlemi bir dosya veya klasör üzerinde hello sağ tooperform olup hello maskesi özelliği hello erişim denetimi algoritması çalışma zamanı toodetermine adresindeki sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="3a9d1-331">Merhaba hello maskesi toocreate "etkili izinleri" Merhaba erişim denetimi anda rolüdür.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="3a9d1-332">Merhaba umask erişim denetimi sırasında hiç kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="3a9d1-333">Merhaba umask kullanılan toodetermine hello erişim ACL bir klasörün yeni alt öğelerinin ' dir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="3a9d1-334">Merhaba maskesi toonamed kullanıcı, adlandırılmış grup ve sahibi olan kullanıcı erişim denetimi hello aynı anda uygulayan bir 3-bit'lik RWX değerdir.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="3a9d1-335">Merhaba umask toohello sorumlu grubu, kullanıcı, geçerli bir 9 bit değerdir ve **diğer** yeni bir alt.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="3a9d1-336">POSIX erişim denetimi modeli hakkında daha fazla bilgiyi nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="3a9d1-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="3a9d1-337">Linux üzerinde POSIX Erişim Denetim Listeleri</span><span class="sxs-lookup"><span data-stu-id="3a9d1-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="3a9d1-338">HDFS izin kılavuzu</span><span class="sxs-lookup"><span data-stu-id="3a9d1-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="3a9d1-339">POSIX SSS</span><span class="sxs-lookup"><span data-stu-id="3a9d1-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="3a9d1-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="3a9d1-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="3a9d1-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="3a9d1-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="3a9d1-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="3a9d1-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="3a9d1-343">Ubuntu üzerinde POSIX ACL</span><span class="sxs-lookup"><span data-stu-id="3a9d1-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="3a9d1-344">Linux üzerinde erişim denetim listelerini kullanan ACL</span><span class="sxs-lookup"><span data-stu-id="3a9d1-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="3a9d1-345">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="3a9d1-345">See also</span></span>

* [<span data-ttu-id="3a9d1-346">Azure Data Lake Store'a Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3a9d1-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
