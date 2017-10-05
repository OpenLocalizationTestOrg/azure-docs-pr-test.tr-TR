---
title: "Data Lake Store’da erişim denetimine genel bakış | Microsoft Belgeleri"
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
ms.openlocfilehash: 99fbad770290d280bdec490d988391ad276ce1ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="c0cbd-103">Azure Data Lake Store’da erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="c0cbd-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="c0cbd-104">Azure Data Lake Store; HDFS ve sonuç olarak POSIX erişim denetimi modelinden türetilen bir erişim denetimi modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from the POSIX access control model.</span></span> <span data-ttu-id="c0cbd-105">Bu makalede Data Lake Store için erişim denetimi modelinin temel bilgileri özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-105">This article summarizes the basics of the access control model for Data Lake Store.</span></span> <span data-ttu-id="c0cbd-106">HDFS erişim denetimi modeli hakkında daha fazla bilgi için bkz. [HDFS İzinleri Kılavuzu](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="c0cbd-106">To learn more about the HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="c0cbd-107">Dosyalar ve klasörler üzerindeki erişim denetimi listeleri</span><span class="sxs-lookup"><span data-stu-id="c0cbd-107">Access control lists on files and folders</span></span>

<span data-ttu-id="c0cbd-108">İki tür erişim denetim listesi (ACL) vardır: **Erişim ACL’leri** ve **Varsayılan ACL’ler**.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="c0cbd-109">**Erişim ACL’leri**: Bunlar bir nesneye erişimi denetler.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-109">**Access ACLs**: These control access to an object.</span></span> <span data-ttu-id="c0cbd-110">Hem dosyalar hem de klasörler Erişim ACL’lerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="c0cbd-111">**Varsayılan ACL’ler**: Bir klasör ile ilişkili olan ACL’lerin o klasör altında oluşturulan tüm alt öğelere ilişkin Erişim ACL’lerini belirleyen bir "şablonudur".</span><span class="sxs-lookup"><span data-stu-id="c0cbd-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine the Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="c0cbd-112">Dosyalar Varsayılan ACL’ye sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-112">Files do not have Default ACLs.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="c0cbd-114">Hem Erişim ACL'leri hem de Varsayılan ACL'ler aynı yapıdadır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-114">Both Access ACLs and Default ACLs have the same structure.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="c0cbd-116">Bir üst öğe üzerindeki Varsayılan ACL’nin değiştirilmesi zaten var olan alt öğelerin Erişim ACL’sini veya Varsayılan ACL’sini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-116">Changing the Default ACL on a parent does not affect the Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="c0cbd-117">Kullanıcılar ve kimlikler</span><span class="sxs-lookup"><span data-stu-id="c0cbd-117">Users and identities</span></span>

<span data-ttu-id="c0cbd-118">Her dosya ve klasör bu kimlikler için farklı izinlere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c0cbd-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="c0cbd-119">Dosyanın sahibi olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="c0cbd-119">The owning user of the file</span></span>
* <span data-ttu-id="c0cbd-120">Sahip olan grup</span><span class="sxs-lookup"><span data-stu-id="c0cbd-120">The owning group</span></span>
* <span data-ttu-id="c0cbd-121">Adlandırılmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="c0cbd-121">Named users</span></span>
* <span data-ttu-id="c0cbd-122">Adlandırılmış gruplar</span><span class="sxs-lookup"><span data-stu-id="c0cbd-122">Named groups</span></span>
* <span data-ttu-id="c0cbd-123">Diğer tüm kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="c0cbd-123">All other users</span></span>

<span data-ttu-id="c0cbd-124">Kullanıcıların ve grupların kimlikleri, Azure Active Directory (Azure AD) kimlikleridir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-124">The identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="c0cbd-125">Bu nedenle, aksi belirtilmediği sürece, Data Lake Store bağlamında "Kullanıcı", Azure AD kullanıcısı veya Azure AD güvenlik grubu olabilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-125">So unless otherwise noted, a "user," in the context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="c0cbd-126">İzinler</span><span class="sxs-lookup"><span data-stu-id="c0cbd-126">Permissions</span></span>

<span data-ttu-id="c0cbd-127">Dosya sistemi nesnesi üzerinde **Okuma**, **Yazma** ve **Yürütme** izinleri bulunur ve bunlar aşağıdaki tabloda gösterildiği gibi dosyalar ve klasörler üzerinde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="c0cbd-127">The permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in the following table:</span></span>

|            |    <span data-ttu-id="c0cbd-128">Dosya</span><span class="sxs-lookup"><span data-stu-id="c0cbd-128">File</span></span>     |   <span data-ttu-id="c0cbd-129">Klasör</span><span class="sxs-lookup"><span data-stu-id="c0cbd-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="c0cbd-130">**Okuma (R)**</span><span class="sxs-lookup"><span data-stu-id="c0cbd-130">**Read (R)**</span></span> | <span data-ttu-id="c0cbd-131">Bir dosyanın içeriğini okuyabilir</span><span class="sxs-lookup"><span data-stu-id="c0cbd-131">Can read the contents of a file</span></span> | <span data-ttu-id="c0cbd-132">Klasörün içeriğini listelemek için **Okuma** ve **Yürütme** izinlerini gerektirir</span><span class="sxs-lookup"><span data-stu-id="c0cbd-132">Requires **Read** and **Execute** to list the contents of the folder</span></span>|
| <span data-ttu-id="c0cbd-133">**Yazma (W)**</span><span class="sxs-lookup"><span data-stu-id="c0cbd-133">**Write (W)**</span></span> | <span data-ttu-id="c0cbd-134">Bir dosyaya yazabilir veya ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="c0cbd-134">Can write or append to a file</span></span> | <span data-ttu-id="c0cbd-135">Bir klasörde alt öğeler oluşturmak için **Yazma** ve **Yürütme** gerektirir</span><span class="sxs-lookup"><span data-stu-id="c0cbd-135">Requires **Write** and **Execute** to create child items in a folder</span></span> |
| <span data-ttu-id="c0cbd-136">**Yürütme (X)**</span><span class="sxs-lookup"><span data-stu-id="c0cbd-136">**Execute (X)**</span></span> | <span data-ttu-id="c0cbd-137">Data Lake Store bağlamında herhangi bir anlamı yoktur</span><span class="sxs-lookup"><span data-stu-id="c0cbd-137">Does not mean anything in the context of Data Lake Store</span></span> | <span data-ttu-id="c0cbd-138">Bir klasörün alt öğelerini geçirmek için gereklidir</span><span class="sxs-lookup"><span data-stu-id="c0cbd-138">Required to traverse the child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="c0cbd-139">İzinlerin kısaltmaları</span><span class="sxs-lookup"><span data-stu-id="c0cbd-139">Short forms for permissions</span></span>

<span data-ttu-id="c0cbd-140">**RWX**, **Okuma + Yazma + Yürütme** için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-140">**RWX** is used to indicate **Read + Write + Execute**.</span></span> <span data-ttu-id="c0cbd-141">**Okuma=4**, **Yazma=2** ve **Yürütme=1** olup toplamları izinleri temsil eden daha da kısaltılmış bir sayısal biçim mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, the sum of which represents the permissions.</span></span> <span data-ttu-id="c0cbd-142">Bazı örnekler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-142">Following are some examples.</span></span>

| <span data-ttu-id="c0cbd-143">Sayısal biçim</span><span class="sxs-lookup"><span data-stu-id="c0cbd-143">Numeric form</span></span> | <span data-ttu-id="c0cbd-144">Kısa biçim</span><span class="sxs-lookup"><span data-stu-id="c0cbd-144">Short form</span></span> |      <span data-ttu-id="c0cbd-145">Anlamı</span><span class="sxs-lookup"><span data-stu-id="c0cbd-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="c0cbd-146">7</span><span class="sxs-lookup"><span data-stu-id="c0cbd-146">7</span></span>            | <span data-ttu-id="c0cbd-147">RWX</span><span class="sxs-lookup"><span data-stu-id="c0cbd-147">RWX</span></span>        | <span data-ttu-id="c0cbd-148">Okuma + Yazma + Yürütme</span><span class="sxs-lookup"><span data-stu-id="c0cbd-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="c0cbd-149">5</span><span class="sxs-lookup"><span data-stu-id="c0cbd-149">5</span></span>            | <span data-ttu-id="c0cbd-150">R-X</span><span class="sxs-lookup"><span data-stu-id="c0cbd-150">R-X</span></span>        | <span data-ttu-id="c0cbd-151">Okuma + Yürütme</span><span class="sxs-lookup"><span data-stu-id="c0cbd-151">Read + Execute</span></span>         |
| <span data-ttu-id="c0cbd-152">4</span><span class="sxs-lookup"><span data-stu-id="c0cbd-152">4</span></span>            | <span data-ttu-id="c0cbd-153">R--</span><span class="sxs-lookup"><span data-stu-id="c0cbd-153">R--</span></span>        | <span data-ttu-id="c0cbd-154">Okuma</span><span class="sxs-lookup"><span data-stu-id="c0cbd-154">Read</span></span>                   |
| <span data-ttu-id="c0cbd-155">0</span><span class="sxs-lookup"><span data-stu-id="c0cbd-155">0</span></span>            | ---        | <span data-ttu-id="c0cbd-156">İzin yok</span><span class="sxs-lookup"><span data-stu-id="c0cbd-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="c0cbd-157">İzinler devralınmaz</span><span class="sxs-lookup"><span data-stu-id="c0cbd-157">Permissions do not inherit</span></span>

<span data-ttu-id="c0cbd-158">Data Lake Store tarafından kullanılan POSIX stili modelinde bir öğenin izinleri öğenin kendisine depolanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-158">In the POSIX-style model that's used by Data Lake Store, permissions for an item are stored on the item itself.</span></span> <span data-ttu-id="c0cbd-159">Diğer bir deyişle, bir öğenin izinleri üst öğelerinden devralınamaz.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-159">In other words, permissions for an item cannot be inherited from the parent items.</span></span>

## <a name="common-scenarios-related-to-permissions"></a><span data-ttu-id="c0cbd-160">İzinlerle ilgili yaygın senaryolar</span><span class="sxs-lookup"><span data-stu-id="c0cbd-160">Common scenarios related to permissions</span></span>

<span data-ttu-id="c0cbd-161">Bir Data Lake Store hesabı üzerinde belirli işlemlerin gerçekleştirilmesi için gereken izinleri anlamanıza yardımcı olacak bazı yaygın senaryolar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-161">Following are some common scenarios to help you understand which permissions are needed to perform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-to-read-a-file"></a><span data-ttu-id="c0cbd-162">Bir dosyayı okumak için gereken izinler</span><span class="sxs-lookup"><span data-stu-id="c0cbd-162">Permissions needed to read a file</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="c0cbd-164">Dosyanın okunması için çağıranın **Okuma** izinlerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-164">For the file to be read, the caller needs **Read** permissions.</span></span>
* <span data-ttu-id="c0cbd-165">Dosyayı içeren klasör yapısındaki tüm klasörler için çağıranın **Yürütme** izinlerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-165">For all the folders in the folder structure that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-append-to-a-file"></a><span data-ttu-id="c0cbd-166">Bir dosyaya eklemek için gereken izinler</span><span class="sxs-lookup"><span data-stu-id="c0cbd-166">Permissions needed to append to a file</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="c0cbd-168">Eklemenin yapılacağı dosya için çağıranın **Yazma** izinlerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-168">For the file to be appended to, the caller needs **Write** permissions.</span></span>
* <span data-ttu-id="c0cbd-169">Dosyayı içeren tüm klasörler için çağıranın **Yürütme** izinlerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-169">For all the folders that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-delete-a-file"></a><span data-ttu-id="c0cbd-170">Bir dosyayı silmek için gereken izinler</span><span class="sxs-lookup"><span data-stu-id="c0cbd-170">Permissions needed to delete a file</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="c0cbd-172">Üst klasör için çağıranın **Yazma + Yürütme** izinlerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-172">For the parent folder, the caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="c0cbd-173">Dosyanın yolundaki diğer tüm klasörler için çağıranın **Yürütme** izinlerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-173">For all the other folders in the file’s path, the caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="c0cbd-174">Önceki iki koşul geçerli oldukça dosyayı silmek için dosya üzerinde yazma izinleri gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-174">Write permissions on the file are not required to delete it as long as the previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-to-enumerate-a-folder"></a><span data-ttu-id="c0cbd-175">Bir klasörü listelemek için gereken izinler</span><span class="sxs-lookup"><span data-stu-id="c0cbd-175">Permissions needed to enumerate a folder</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="c0cbd-177">Listelenecek klasör için çağıranın **Okuma + Yürütme** izinlerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-177">For the folder to enumerate, the caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="c0cbd-178">Tüm üst klasörler için çağıranın **Yürütme** izinlerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-178">For all the ancestor folders, the caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-the-azure-portal"></a><span data-ttu-id="c0cbd-179">Azure portalında görüntüleme izinleri</span><span class="sxs-lookup"><span data-stu-id="c0cbd-179">Viewing permissions in the Azure portal</span></span>

<span data-ttu-id="c0cbd-180">Data Lake Store hesabının **Veri Gezgini** dikey penceresinde **Erişim**’e tıklayarak bir dosya veya klasörün ACL’lerini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-180">From the **Data Explorer** blade of the Data Lake Store account, click **Access** to see the ACLs for a file or a folder.</span></span> <span data-ttu-id="c0cbd-181">**mydatastore** hesabı altındaki **catalog** klasörüne ilişkin ACL’leri görmek için **Erişim**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-181">Click **Access** to see the ACLs for the **catalog** folder under the **mydatastore** account.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="c0cbd-183">Bu dikey pencerenin üst tarafında sahip olduğunuz izinlerin özeti gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-183">On this blade, the top section shows an overview of the permissions that you have.</span></span> <span data-ttu-id="c0cbd-184">(Ekran görüntüsünde Bob kullanıcıdır.) Bunun altında erişim izinleri gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-184">(In the screenshot, the user is Bob.) Following that, the access permissions are shown.</span></span> <span data-ttu-id="c0cbd-185">Bundan sonra **Erişim** dikey penceresinde **Basit Görünüm**’e tıklayarak daha basit bir görünüm görün.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-185">After that, from the **Access** blade, click **Simple View** to see the simpler view.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="c0cbd-187">Varsayılan ACL’ler, maske ve süper kullanıcı kavramlarının gösterildiği daha gelişmiş görünümü görmek için **Gelişmiş Görünüm**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-187">Click **Advanced View** to see the more advanced view, where the concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="the-super-user"></a><span data-ttu-id="c0cbd-189">Süper kullanıcı</span><span class="sxs-lookup"><span data-stu-id="c0cbd-189">The super-user</span></span>

<span data-ttu-id="c0cbd-190">Süper kullanıcı, Data Lake Store’daki tüm kullanıcılar arasında en fazla hakka sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-190">A super-user has the most rights of all the users in the Data Lake Store.</span></span> <span data-ttu-id="c0cbd-191">Süper kullanıcı:</span><span class="sxs-lookup"><span data-stu-id="c0cbd-191">A super-user:</span></span>

* <span data-ttu-id="c0cbd-192">**Tüm** dosya ve klasörlerde RWX İzinlerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-192">Has RWX Permissions to **all** files and folders.</span></span>
* <span data-ttu-id="c0cbd-193">Herhangi bir dosya veya klasörün izinlerini değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-193">Can change the permissions on any file or folder.</span></span>
* <span data-ttu-id="c0cbd-194">Herhangi bir dosya veya klasörün sahibi olan kullanıcıyı ya da grubu değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-194">Can change the owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="c0cbd-195">Azure’da bir Data Lake Store hesabının birkaç Azure rolü vardır, bunlar:</span><span class="sxs-lookup"><span data-stu-id="c0cbd-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="c0cbd-196">Sahipler</span><span class="sxs-lookup"><span data-stu-id="c0cbd-196">Owners</span></span>
* <span data-ttu-id="c0cbd-197">Katkıda Bulunanlar</span><span class="sxs-lookup"><span data-stu-id="c0cbd-197">Contributors</span></span>
* <span data-ttu-id="c0cbd-198">Okuyucular</span><span class="sxs-lookup"><span data-stu-id="c0cbd-198">Readers</span></span>

<span data-ttu-id="c0cbd-199">Bir Data Lake Store hesabında **Sahipler** rolündeki herkes otomatik olarak o hesabın süper kullanıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-199">Everyone in the **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="c0cbd-200">Daha fazla bilgi için bkz. [Rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0cbd-200">To learn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="c0cbd-201">Süper kullanıcı izinlerine sahip özel bir rol tabanlı erişim denetimi (RBAC) rolü oluşturmak isterseniz şu izinleri vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c0cbd-201">If you want to create a custom role-based-access control (RBAC) role that has super-user permissions, it needs to have the following permissions:</span></span>
- <span data-ttu-id="c0cbd-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="c0cbd-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="c0cbd-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="c0cbd-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="the-owning-user"></a><span data-ttu-id="c0cbd-204">Sahip olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="c0cbd-204">The owning user</span></span>

<span data-ttu-id="c0cbd-205">Öğeyi oluşturan kullanıcı otomatik olarak öğenin sahibi olan kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-205">The user who created the item is automatically the owning user of the item.</span></span> <span data-ttu-id="c0cbd-206">Sahip olan kullanıcı şunları yapabilir:</span><span class="sxs-lookup"><span data-stu-id="c0cbd-206">An owning user can:</span></span>

* <span data-ttu-id="c0cbd-207">Sahip olunan bir dosyanın izinlerini değiştirme.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-207">Change the permissions of a file that is owned.</span></span>
* <span data-ttu-id="c0cbd-208">Sahip olan kullanıcı aynı zamanda hedef grubun bir üyesi oldukça, sahip olunan bir dosyanın sahibi olan grubunu değiştirme.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-208">Change the owning group of a file that is owned, as long as the owning user is also a member of the target group.</span></span>

> [!NOTE]
> <span data-ttu-id="c0cbd-209">Sahip olan kullanıcı başka bir sahibi olunan dosyanın sahibini *değiştiremez*.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-209">The owning user *cannot* change the owning user of another owned file.</span></span> <span data-ttu-id="c0cbd-210">Bir dosya veya klasörün sahibi olan kullanıcıyı yalnızca süper kullanıcılar değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-210">Only super-users can change the owning user of a file or folder.</span></span>
>
>

## <a name="the-owning-group"></a><span data-ttu-id="c0cbd-211">Sahip olan grup</span><span class="sxs-lookup"><span data-stu-id="c0cbd-211">The owning group</span></span>

<span data-ttu-id="c0cbd-212">POSIX ACL’lerinde her kullanıcı bir "birincil grup" ile ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-212">In the POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="c0cbd-213">Örneğin, "gamze" adlı kullanıcı "finans" grubuna ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-213">For example, user "alice" might belong to the "finance" group.</span></span> <span data-ttu-id="c0cbd-214">Gamze ayrıca birden fazla gruba ait olabilir, ancak bir grup her zaman birincil grubu olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-214">Alice might also belong to multiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="c0cbd-215">POSIX’te Gamze bir dosya oluşturduğunda o dosyanın sahibi olan grup birincil grubu olarak ayarlanır (bu örnekte "finans" grubudur).</span><span class="sxs-lookup"><span data-stu-id="c0cbd-215">In POSIX, when Alice creates a file, the owning group of that file is set to her primary group, which in this case is "finance."</span></span>

<span data-ttu-id="c0cbd-216">Yeni bir dosya sistemi öğesi oluşturulduğunda, Data Lake Store sahip olan gruba bir değer atar.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-216">When a new filesystem item is created, Data Lake Store assigns a value to the owning group.</span></span>

* <span data-ttu-id="c0cbd-217">**Olay 1**: Kök klasör "/".</span><span class="sxs-lookup"><span data-stu-id="c0cbd-217">**Case 1**: The root folder "/".</span></span> <span data-ttu-id="c0cbd-218">Bir Data Lake Store hesabı oluşturulduğunda bu klasör oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="c0cbd-219">Bu durumda sahip olan grup, hesabı oluşturan kullanıcıya ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-219">In this case, the owning group is set to the user who created the account.</span></span>
* <span data-ttu-id="c0cbd-220">**Olay 2** (Diğer her olay): Yeni bir olay oluşturulduğunda sahip olan grup üst klasörden kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-220">**Case 2** (Every other case): When a new item is created, the owning group is copied from the parent folder.</span></span>

<span data-ttu-id="c0cbd-221">Sahip olan grup aşağıdakiler tarafından değiştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="c0cbd-221">The owning group can be changed by:</span></span>
* <span data-ttu-id="c0cbd-222">Herhangi bir süper kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-222">Any super-users.</span></span>
* <span data-ttu-id="c0cbd-223">Sahip olan kullanıcı aynı zamanda hedef grubun üyesi ise sahip olan kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-223">The owning user, if the owning user is also a member of the target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="c0cbd-224">Erişim denetimi algoritması</span><span class="sxs-lookup"><span data-stu-id="c0cbd-224">Access check algorithm</span></span>

<span data-ttu-id="c0cbd-225">Aşağıdaki çizimde Data Lake Store hesaplarına yönelik erişim denetimi algoritması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-225">The following illustration represents the access check algorithm for Data Lake Store accounts.</span></span>

![Data Lake Store ACL’leri algoritması](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="the-mask-and-effective-permissions"></a><span data-ttu-id="c0cbd-227">Maske ve "etkili izinler"</span><span class="sxs-lookup"><span data-stu-id="c0cbd-227">The mask and "effective permissions"</span></span>

<span data-ttu-id="c0cbd-228">**Maske**, erişim denetimi algoritmasını gerçekleştirirken **adlandırılmış kullanıcılar**, **sahip olan grup** ve **adlandırılmış gruplar** için erişimi sınırlandırmak üzere kullanılan bir RWX değeridir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-228">The **mask** is an RWX value that is used to limit access for **named users**, the **owning group**, and **named groups** when you're performing the access check algorithm.</span></span> <span data-ttu-id="c0cbd-229">Maskeye ilişkin anahtar kavramlar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-229">Here are the key concepts for the mask.</span></span>

* <span data-ttu-id="c0cbd-230">Maske, "etkili izinleri" oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-230">The mask creates "effective permissions."</span></span> <span data-ttu-id="c0cbd-231">Diğer bir deyişle, erişim denetimi zamanında izinleri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-231">That is, it modifies the permissions at the time of access check.</span></span>
* <span data-ttu-id="c0cbd-232">Maske doğrudan dosya sahibi ve herhangi bir süper kullanıcı tarafından düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-232">The mask can be directly edited by the file owner and any super-users.</span></span>
* <span data-ttu-id="c0cbd-233">Maske etkili izin oluşturmaya yönelik izinleri kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-233">The mask can remove permissions to create the effective permission.</span></span> <span data-ttu-id="c0cbd-234">Maske etkili izne izinler *ekleyemez*.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-234">The mask *cannot* add permissions to the effective permission.</span></span>

<span data-ttu-id="c0cbd-235">Bazı örneklere bakalım.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-235">Let's look at some examples.</span></span> <span data-ttu-id="c0cbd-236">Aşağıdaki örnekte maske **RWX** olarak ayarlanmıştır. Diğer bir deyişle maske herhangi bir izni kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-236">In the following example, the mask is set to **RWX**, which means that the mask does not remove any permissions.</span></span> <span data-ttu-id="c0cbd-237">Adlandırılmış kullanıcı, sahip olan kullanıcı ve adlandırılmış grup, erişim denetimi sırasında değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-237">The effective permissions for the named user, owning group, and named group are not altered during the access check.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="c0cbd-239">Aşağıdaki örnekte maske **R-X** olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-239">In the following example, the mask is set to **R-X**.</span></span> <span data-ttu-id="c0cbd-240">Bu nedenle, erişim denetimi sırasında **adlandırılmış kullanıcı**, **sahip olan grup** ve **adlandırılmış grup** için **Yazma izinlerini kapatır**.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-240">This means that it **turns off the Write permissions** for **named user**, **owning group**, and **named group** at the time of access check.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="c0cbd-242">Başvuru için bir dosyanın veya klasörün maskesinin Azure portalında nerede göründüğü aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-242">For reference, here is where the mask for a file or folder appears in the Azure portal.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="c0cbd-244">Yeni bir Data Lake Store hesabı için kök klasörün ("/") Erişim ACL’si ve Varsayılan ACL’si için maske varsayılan olarak RWX’tir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-244">For a new Data Lake Store account, the mask for the Access ACL and Default ACL of the root folder ("/") defaults to RWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="c0cbd-245">Yeni dosyalar ve klasörler üzerindeki izinler</span><span class="sxs-lookup"><span data-stu-id="c0cbd-245">Permissions on new files and folders</span></span>

<span data-ttu-id="c0cbd-246">Var olan bir klasör altında yeni bir dosya ya da klasör oluşturulduğunda üst klasördeki Varsayılan ACL aşağıdakileri belirler:</span><span class="sxs-lookup"><span data-stu-id="c0cbd-246">When a new file or folder is created under an existing folder, the Default ACL on the parent folder determines:</span></span>

- <span data-ttu-id="c0cbd-247">Bir alt klasörün Varsayılan ACL’si ve Erişim ACL’si.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="c0cbd-248">Bir alt dosyanın Erişim ACL’si (dosyaları Varsayılan ACL’ye sahip değildir).</span><span class="sxs-lookup"><span data-stu-id="c0cbd-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="the-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="c0cbd-249">Bir alt dosya veya klasörün Erişim ACL’si</span><span class="sxs-lookup"><span data-stu-id="c0cbd-249">The Access ACL of a child file or folder</span></span>

<span data-ttu-id="c0cbd-250">Bir alt dosya veya klasör oluşturulduğunda, üst öğenin Varsayılan ACL’si alt dosya veya klasörün Erişim ACL’si olarak kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-250">When a child file or folder is created, the parent's Default ACL is copied as the Access ACL of the child file or folder.</span></span> <span data-ttu-id="c0cbd-251">Ayrıca, **diğer** kullanıcının üst klasör varsayılan ACL’sinde RWX izinleri varsa alt öğenin Erişim ACL’sinden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-251">Also, if **other** user has RWX permissions in the parent's default ACL, it is removed from the child item's Access ACL.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="c0cbd-253">Çoğu senaryoda yukarıdaki bilgiler bir alt öğenin Erişim ACL’sinin belirlenmesi için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-253">In most scenarios, the previous information is all you need to know about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="c0cbd-254">Ancak, POSIX sistemlerini biliyor ve bu bilgilerin nasıl elde edildiğini derinlemesine öğrenmek istiyorsanız bu makalenin sonraki bölümlerinde bulunan [Yeni dosyalar ve klasörler için Erişim ACL’lerini oluşturmada Umask rolü](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) kısmına bakın.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-254">However, if you are familiar with POSIX systems and want to understand in-depth how this transformation is achieved, see the section [Umask’s role in creating the Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="c0cbd-255">Bir alt klasörün Varsayılan ACL’si</span><span class="sxs-lookup"><span data-stu-id="c0cbd-255">A child folder's Default ACL</span></span>

<span data-ttu-id="c0cbd-256">Üst klasör altında bir alt klasör oluşturulduğunda üst klasörün Varsayılan ACL’si olduğu gibi alt klasörün Varsayılan ACL’sine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-256">When a child folder is created under a parent folder, the parent folder's Default ACL is copied over as is to the child folder's Default ACL.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="c0cbd-258">Data Lake Store’da ACL’leri anlamaya yönelik gelişmiş konular</span><span class="sxs-lookup"><span data-stu-id="c0cbd-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="c0cbd-259">Data Lake Store dosyaları veya klasörleri için ACL’lerin nasıl belirlendiğini anlamanıza yardımcı olan birkaç gelişmiş konu aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-259">Following are some advanced topics to help you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-the-access-acl-for-new-files-and-folders"></a><span data-ttu-id="c0cbd-260">Yeni dosyalar ve klasörler için Erişim ACL’lerini oluşturmada Umask rolü</span><span class="sxs-lookup"><span data-stu-id="c0cbd-260">Umask’s role in creating the Access ACL for new files and folders</span></span>

<span data-ttu-id="c0cbd-261">POSIX ile uyumlu bir sistemde genel kavram umask’in yeni bir alt klasör veya klasörün Erişim ACL’si üzerinde **sahip olan kullanıcı**, **sahip olan grup** ve **diğer** iznini dönüştürmek için kullanılan üst klasördeki 9 bitlik bir değer olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-261">In a POSIX-compliant system, the general concept is that umask is a 9-bit value on the parent folder that's used to transform the permission for **owning user**, **owning group**, and **other** on the Access ACL of a new child file or folder.</span></span> <span data-ttu-id="c0cbd-262">Bir umask’in bit değerleri alt öğenin Erişim ACL’sinde hangi bitlerin kapatılacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-262">The bits of a umask identify which bits to turn off in the child item’s Access ACL.</span></span> <span data-ttu-id="c0cbd-263">Bu nedenle **sahip olan kullanıcı**, **sahip olan grup** ve **diğer** için izinlerin yayılmasını seçici olarak önlemek üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-263">Thus it is used to selectively prevent the propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="c0cbd-264">Bir HDFS sisteminde umask genellikle yöneticiler tarafından denetlenen site genelindeki bir yapılandırma seçeneğidir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-264">In an HDFS system, the umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="c0cbd-265">Data Lake Store değiştirilemeyen bir **hesap genelinde umask** kullanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="c0cbd-266">Aşağıdaki tabloda Data Lake Store için umask gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-266">The following table shows the unmask for Data Lake Store.</span></span>

| <span data-ttu-id="c0cbd-267">Kullanıcı grubu</span><span class="sxs-lookup"><span data-stu-id="c0cbd-267">User group</span></span>  | <span data-ttu-id="c0cbd-268">Ayar</span><span class="sxs-lookup"><span data-stu-id="c0cbd-268">Setting</span></span> | <span data-ttu-id="c0cbd-269">Yeni alt öğenin Erişim ACL’si üzerindeki etkisi</span><span class="sxs-lookup"><span data-stu-id="c0cbd-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="c0cbd-270">Sahip olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="c0cbd-270">Owning user</span></span> | ---     | <span data-ttu-id="c0cbd-271">Etki yok</span><span class="sxs-lookup"><span data-stu-id="c0cbd-271">No effect</span></span>                             |
| <span data-ttu-id="c0cbd-272">Sahip olan grup</span><span class="sxs-lookup"><span data-stu-id="c0cbd-272">Owning group</span></span>| ---     | <span data-ttu-id="c0cbd-273">Etki yok</span><span class="sxs-lookup"><span data-stu-id="c0cbd-273">No effect</span></span>                             |
| <span data-ttu-id="c0cbd-274">Diğer</span><span class="sxs-lookup"><span data-stu-id="c0cbd-274">Other</span></span>       | <span data-ttu-id="c0cbd-275">RWX</span><span class="sxs-lookup"><span data-stu-id="c0cbd-275">RWX</span></span>     | <span data-ttu-id="c0cbd-276">Okuma + Yazma + Yürütme iznini kaldırma</span><span class="sxs-lookup"><span data-stu-id="c0cbd-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="c0cbd-277">Aşağıdaki çizimde bu umask eylemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-277">The following illustration shows this umask in action.</span></span> <span data-ttu-id="c0cbd-278">Net etki **diğer** kullanıcı için **Okuma + Yazma + Yürütme** izninin kaldırılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-278">The net effect is to remove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="c0cbd-279">Umask **sahip olan kullanıcı** ve **sahip olan grup** için bitleri belirtmediğinden bu izinler dönüştürülmez.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-279">Because the umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="the-sticky-bit"></a><span data-ttu-id="c0cbd-281">Yapışkan bit</span><span class="sxs-lookup"><span data-stu-id="c0cbd-281">The sticky bit</span></span>

<span data-ttu-id="c0cbd-282">Yapışkan bit POSIX dosya sisteminin daha gelişmiş bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-282">The sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="c0cbd-283">Data Lake Store bağlamında yapışkan bitin gerekli olması düşük bir olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-283">In the context of Data Lake Store, it is unlikely that the sticky bit will be needed.</span></span>

<span data-ttu-id="c0cbd-284">Aşağıdaki tabloda yapışkan bitin Data Lake Store’da nasıl çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-284">The following table shows how the sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="c0cbd-285">Kullanıcı grubu</span><span class="sxs-lookup"><span data-stu-id="c0cbd-285">User group</span></span>         | <span data-ttu-id="c0cbd-286">Dosya</span><span class="sxs-lookup"><span data-stu-id="c0cbd-286">File</span></span>    | <span data-ttu-id="c0cbd-287">Klasör</span><span class="sxs-lookup"><span data-stu-id="c0cbd-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="c0cbd-288">Yapışkan bit **Kapalı**</span><span class="sxs-lookup"><span data-stu-id="c0cbd-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="c0cbd-289">Etki yok</span><span class="sxs-lookup"><span data-stu-id="c0cbd-289">No effect</span></span>   | <span data-ttu-id="c0cbd-290">Etki yok.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-290">No effect.</span></span>           |
| <span data-ttu-id="c0cbd-291">Yapışkan bit **Açık**</span><span class="sxs-lookup"><span data-stu-id="c0cbd-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="c0cbd-292">Etki yok</span><span class="sxs-lookup"><span data-stu-id="c0cbd-292">No effect</span></span>   | <span data-ttu-id="c0cbd-293">Bir alt öğenin **süper kullanıcıları** ve **sahip olan kullanıcısı** dışında herkesin alt öğeyi silmesini veya yeniden adlandırmasını önler.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-293">Prevents anyone except **super-users** and the **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="c0cbd-294">Yapışkan bit Azure portalında gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-294">The sticky bit is not shown in the Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="c0cbd-295">Data Lake Store’daki ACL’ler hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="c0cbd-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="c0cbd-296">Data Lake Store’daki ACL’lerle ilgili olarak sık sorulan bazı sorular aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-to-enable-support-for-acls"></a><span data-ttu-id="c0cbd-297">ACL desteğini etkinleştirmem gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-297">Do I have to enable support for ACLs?</span></span>

<span data-ttu-id="c0cbd-298">Hayır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-298">No.</span></span> <span data-ttu-id="c0cbd-299">ACL’ler üzerinden erişim denetimi Data Lake Store hesabı için her zaman açıktır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-to-recursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="c0cbd-300">Bir klasörü ve içindekileri yinelemeli olarak silmek için hangi izinler gereklidir?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-300">Which permissions are required to recursively delete a folder and its contents?</span></span>

* <span data-ttu-id="c0cbd-301">Üst klasör **Yazma + Yürütme** izinlerine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-301">The parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="c0cbd-302">Silinecek klasör ve içindeki her klasör **Okuma + Yazma + Yürütme** izinlerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-302">The folder to be deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="c0cbd-303">Klasörlerdeki dosyaları silmek için Yazma izni gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-303">You do not need Write permissions to delete files in folders.</span></span> <span data-ttu-id="c0cbd-304">Ayrıca, "/" kök klasör **hiçbir zaman** silinemez.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-304">Also, the root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-the-owner-of-a-file-or-folder"></a><span data-ttu-id="c0cbd-305">Bir dosyanın veya klasörün sahibi kimdir?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-305">Who is the owner of a file or folder?</span></span>

<span data-ttu-id="c0cbd-306">Bir dosyayı veya klasörü oluşturan kişi bunların sahibi olur.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-306">The creator of a file or folder becomes the owner.</span></span>

### <a name="which-group-is-set-as-the-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="c0cbd-307">Oluşturma sırasında bir dosyanın veya klasörün sahibi olan grubu olarak hangi grup ayarlanır?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-307">Which group is set as the owning group of a file or folder at creation?</span></span>

<span data-ttu-id="c0cbd-308">Sahip olan grup, yeni dosya veya klasörün oluşturulduğu üst klasörün sahibi olan gruptan kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-308">The owning group is copied from the owning group of the parent folder under which the new file or folder is created.</span></span>

### <a name="i-am-the-owning-user-of-a-file-but-i-dont-have-the-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="c0cbd-309">Bir dosyanın sahibiyim, ancak gereken RWX izinlerine sahip değilim.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-309">I am the owning user of a file but I don’t have the RWX permissions I need.</span></span> <span data-ttu-id="c0cbd-310">Ne yapmalıyım?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-310">What do I do?</span></span>

<span data-ttu-id="c0cbd-311">Sahip olan kullanıcı kendisine gerekli olan her türlü RWX iznini vermek için dosyanın izinlerini değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-311">The owning user can change the permissions of the file to give themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-the-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="c0cbd-312">Azure portalında ACL’lere baktığımda kullanıcı adlarını görüyorum, ancak API’lere baktığımda GUID’leri görüyorum, bunun nedeni nedir?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-312">When I look at ACLs in the Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="c0cbd-313">ACL’lerdeki girişler, Azure AD’de kullanıcılara karşılık gelen GUID’ler olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-313">Entries in the ACLs are stored as GUIDs that correspond to users in Azure AD.</span></span> <span data-ttu-id="c0cbd-314">API’ler GUID’leri olduğu gibi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-314">The APIs return the GUIDs as is.</span></span> <span data-ttu-id="c0cbd-315">Azure portalı mümkün olduğunda GUID’leri kolay adlara çevirerek ACL’lerin daha kolay kullanılmasını sağlamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-315">The Azure portal tries to make ACLs easier to use by translating the GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-the-acls-when-im-using-the-azure-portal"></a><span data-ttu-id="c0cbd-316">Azure portalını kullanırken neden bazen ACL’lerde GUID’leri görüyorum?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-316">Why do I sometimes see GUIDs in the ACLs when I'm using the Azure portal?</span></span>

<span data-ttu-id="c0cbd-317">Kullanıcı artık Azure AD’de mevcut değilse bir GUID gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-317">A GUID is shown when the user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="c0cbd-318">Bu genellikle, kullanıcı şirketten ayrıldığında veya Azure AD’de kullanıcının hesabı silindiğinde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-318">Usually this happens when the user has left the company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="c0cbd-319">Data Lake Store ACL’lerin devralınmasını destekler mi?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="c0cbd-320">Hayır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-320">No.</span></span>

### <a name="what-is-the-difference-between-mask-and-umask"></a><span data-ttu-id="c0cbd-321">Maske ile umask arasındaki fark nedir?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-321">What is the difference between mask and umask?</span></span>

| <span data-ttu-id="c0cbd-322">maske</span><span class="sxs-lookup"><span data-stu-id="c0cbd-322">mask</span></span> | <span data-ttu-id="c0cbd-323">umask</span><span class="sxs-lookup"><span data-stu-id="c0cbd-323">umask</span></span>|
|------|------|
| <span data-ttu-id="c0cbd-324">**Maske** özelliği her dosya ve klasörde bulunur.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-324">The **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="c0cbd-325">**Umask** ise Data Lake Store hesabının bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-325">The **umask** is a property of the Data Lake Store account.</span></span> <span data-ttu-id="c0cbd-326">Bu nedenle, Data Lake Store’de yalnızca tek bir umask vardır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-326">So there is only a single umask in the Data Lake Store.</span></span>    |
| <span data-ttu-id="c0cbd-327">Bir dosya veya klasördeki maske özelliği, dosyanın sahibi olan kullanıcı veya grup ya da süper kullanıcı tarafından değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-327">The mask property on a file or folder can be altered by the owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="c0cbd-328">Umask özelliği ise süper kullanıcı dahil hiçbir kullanıcı tarafından değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-328">The umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="c0cbd-329">Bu özellik, değiştirilemeyen sabit bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="c0cbd-330">Maske özelliği bir kullanıcının dosya ya da klasör üzerinde işlem gerçekleştirme hakkına sahip olup olmadığını belirlemek üzere çalışma zamanındaki erişim denetimi algoritması sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-330">The mask property is used during the access check algorithm at runtime to determine whether a user has the right to perform on operation on a file or folder.</span></span> <span data-ttu-id="c0cbd-331">Maskenin rolü, erişim denetimi sırasında "etkili izinleri" oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-331">The role of the mask is to create "effective permissions" at the time of access check.</span></span> | <span data-ttu-id="c0cbd-332">Umask, erişim denetimi sırasında hiç kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-332">The umask is not used during access check at all.</span></span> <span data-ttu-id="c0cbd-333">Umask bir klasörün yeni alt öğelerinin Erişim ACL’sini belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-333">The umask is used to determine the Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="c0cbd-334">Maske; erişim denetimi sırasında adlandırılmış kullanıcı, adlandırılmış grup ve sahip olan kullanıcı için geçerli olan 3 bitlik bir RWX değeridir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-334">The mask is a 3-bit RWX value that applies to named user, named group, and owning user at the time of access check.</span></span>| <span data-ttu-id="c0cbd-335">Umask ise yeni bir alt öğenin sahip olan kullanıcı, sahip olan grup ve **diğer** kullanıcısı için geçerli olan 9 bitlik bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-335">The umask is a 9-bit value that applies to the owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="c0cbd-336">POSIX erişim denetimi modeli hakkında daha fazla bilgiyi nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="c0cbd-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="c0cbd-337">Linux üzerinde POSIX Erişim Denetim Listeleri</span><span class="sxs-lookup"><span data-stu-id="c0cbd-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="c0cbd-338">HDFS izin kılavuzu</span><span class="sxs-lookup"><span data-stu-id="c0cbd-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="c0cbd-339">POSIX SSS</span><span class="sxs-lookup"><span data-stu-id="c0cbd-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="c0cbd-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="c0cbd-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="c0cbd-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="c0cbd-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="c0cbd-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="c0cbd-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="c0cbd-343">Ubuntu üzerinde POSIX ACL</span><span class="sxs-lookup"><span data-stu-id="c0cbd-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="c0cbd-344">Linux üzerinde erişim denetim listelerini kullanan ACL</span><span class="sxs-lookup"><span data-stu-id="c0cbd-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="c0cbd-345">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c0cbd-345">See also</span></span>

* [<span data-ttu-id="c0cbd-346">Azure Data Lake Store'a Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c0cbd-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
