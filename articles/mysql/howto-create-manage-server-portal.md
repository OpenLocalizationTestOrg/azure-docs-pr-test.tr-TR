---
title: "aaaCreate ve MySQL sunucusu için Azure portalını kullanarak Azure veritabanını yönetme | Microsoft Docs"
description: "Bu makalede nasıl hızlı bir şekilde MySQL sunucusu için yeni bir Azure veritabanı oluşturabilir ve hello sunucuyu hello Azure Portal kullanarak yönetiyorsanız açıklanmaktadır."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="20202-103">Oluşturma ve Azure veritabanı MySQL sunucusu için Azure portalını kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="20202-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="20202-104">Bu makalede nasıl hızlı bir şekilde MySQL sunucusu için yeni bir Azure veritabanı oluşturabilir ve hello sunucuyu hello Azure Portal kullanarak yönetiyorsanız açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="20202-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="20202-105">Sunucu Yönetimi Sunucusu ayrıntılarını & veritabanları görüntüleme, parola sıfırlama ve hello sunucuyu silmek içerir.</span><span class="sxs-lookup"><span data-stu-id="20202-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="20202-106">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="20202-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="20202-107">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20202-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="20202-108">MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="20202-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="20202-109">Bu adımları toocreate "mysqlserver4demo" adlı MySQL sunucusu için bir Azure veritabanı izleyin</span><span class="sxs-lookup"><span data-stu-id="20202-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="20202-110">1-tıklatma **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="20202-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="20202-111">2-seçin **veritabanları** hello yeni sayfa ve select **Azure veritabanı için MySQL** hello veritabanları sayfasından.</span><span class="sxs-lookup"><span data-stu-id="20202-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="20202-112">MySQL sunucusu için bir Azure veritabanı tanımlanan bir dizi ile oluşturulan [işlem ve depolama](./concepts-compute-unit-and-storage.md) kaynakları.</span><span class="sxs-lookup"><span data-stu-id="20202-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="20202-113">Merhaba veritabanı, MySQL sunucusu için bir Azure veritabanında, bir Azure kaynak grubu içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="20202-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![Yeni-sunucusu oluştur](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="20202-115">3 - hello Azure veritabanı MySQL form için aşağıdaki bilgilerle hello ile doldurun:</span><span class="sxs-lookup"><span data-stu-id="20202-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="20202-116">**Form Alanı**</span><span class="sxs-lookup"><span data-stu-id="20202-116">**Form Field**</span></span> | <span data-ttu-id="20202-117">**Alan Açıklaması**</span><span class="sxs-lookup"><span data-stu-id="20202-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="20202-118">*Sunucu adı*</span><span class="sxs-lookup"><span data-stu-id="20202-118">*Server name*</span></span> | <span data-ttu-id="20202-119">Azure mysql (sunucu adı genel olarak benzersiz)</span><span class="sxs-lookup"><span data-stu-id="20202-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="20202-120">*Abonelik*</span><span class="sxs-lookup"><span data-stu-id="20202-120">*Subscription*</span></span> | <span data-ttu-id="20202-121">MySQLaaS (açılan seçin)</span><span class="sxs-lookup"><span data-stu-id="20202-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="20202-122">*Kaynak grubu*</span><span class="sxs-lookup"><span data-stu-id="20202-122">*Resource group*</span></span> | <span data-ttu-id="20202-123">myresource (yeni bir kaynak grubu oluşturun veya var olanı kullanırsınız)</span><span class="sxs-lookup"><span data-stu-id="20202-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="20202-124">*Sunucu yöneticisi oturum açma bilgileri*</span><span class="sxs-lookup"><span data-stu-id="20202-124">*Server admin login*</span></span> | <span data-ttu-id="20202-125">myadmin (yönetici hesabı adını ayarlayın)</span><span class="sxs-lookup"><span data-stu-id="20202-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="20202-126">*Parola*</span><span class="sxs-lookup"><span data-stu-id="20202-126">*Password*</span></span> | <span data-ttu-id="20202-127">Kurulum yönetici hesabı parolası</span><span class="sxs-lookup"><span data-stu-id="20202-127">setup admin account password</span></span> |
| <span data-ttu-id="20202-128">*Parolayı onayla*</span><span class="sxs-lookup"><span data-stu-id="20202-128">*Confirm password*</span></span> | <span data-ttu-id="20202-129">yönetici hesabı parolasını onaylayın</span><span class="sxs-lookup"><span data-stu-id="20202-129">confirm admin account password</span></span> |
| <span data-ttu-id="20202-130">*Konum*</span><span class="sxs-lookup"><span data-stu-id="20202-130">*Location*</span></span> | <span data-ttu-id="20202-131">Kuzey Avrupa (Kuzey Avrupa ve Batı ABD arasında seçim)</span><span class="sxs-lookup"><span data-stu-id="20202-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="20202-132">*Sürüm*</span><span class="sxs-lookup"><span data-stu-id="20202-132">*Version*</span></span> | <span data-ttu-id="20202-133">5.6 (Azure veritabanı için MySQL sunucusu sürümü seçin)</span><span class="sxs-lookup"><span data-stu-id="20202-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="20202-134">4-tıklatın **fiyatlandırma katmanı** toospecify hello Hizmet katmanını ve performans düzeyini yeni sunucunuzu.</span><span class="sxs-lookup"><span data-stu-id="20202-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="20202-135">İşlem birim 50 ile temel katman, 100 ve 200 standart katmanındaki ile 100 arasında yapılandırılabilir ve depolama dahil edilen miktar bağlı olarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="20202-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="20202-136">Bu nasıl yapılır kılavuzu için şimdi bir 50 işlem birimi ve 50 GB'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="20202-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="20202-137">Tıklatın **Tamam** toosave seçiminizi.</span><span class="sxs-lookup"><span data-stu-id="20202-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="20202-138">![oluşturma sunucu-fiyatlandırma-katmanı](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="20202-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="20202-139">5'i tıklatın **oluşturma** tooprovision hello sunucu.</span><span class="sxs-lookup"><span data-stu-id="20202-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="20202-140">Sağlama birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="20202-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="20202-141">Merhaba denetleyin **PIN toodashboard** seçeneği tooallow kolay izlenmesini dağıtımlarınızı.</span><span class="sxs-lookup"><span data-stu-id="20202-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="20202-142">Temel katmanındaki too1000GB ve 10000 GB standart katmanı depolama için genel Önizleme için desteklenecek hello maksimum depolama hala sınırlı too1000GB geçici olarak olsa.</span><span class="sxs-lookup"><span data-stu-id="20202-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="20202-143">MySQL sunucusu için bir Azure veritabanını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="20202-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="20202-144">Yeni Sunucu sağlandıktan sonra kullanıcı 2 seçenekleri tooedit varolan sunucusu vardır.: sıfırlama yönetici parolası veya ölçek yukarı/aşağı hello sunucu hello işlem-birimleri değiştirerek.</span><span class="sxs-lookup"><span data-stu-id="20202-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="20202-145">Hello Yöneticisi kullanıcı parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="20202-145">Change hello administrator user password</span></span>
<span data-ttu-id="20202-146">1 - sunucuda hello **genel bakış** dikey penceresinde tıklatın **parola sıfırlama** toopopulate bir parola giriş ve onay penceresi.</span><span class="sxs-lookup"><span data-stu-id="20202-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="20202-147">2 - yeni bir parola girin ve aşağıdaki şekilde hello penceresinde hello parolayı onaylayın: ![parola sıfırlama](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="20202-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="20202-148">3-tıklatın **Tamam** toosave hello yeni parola.</span><span class="sxs-lookup"><span data-stu-id="20202-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="20202-149">Ölçek yukarı/aşağı işlem birimleri değiştirerek</span><span class="sxs-lookup"><span data-stu-id="20202-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="20202-150">1 - üzerinde hello sunucu dikey altında **ayarları**, tıklatın **fiyatlandırma katmanı** tooopen hello fiyatlandırma katmanı dikey hello Azure veritabanı MySQL sunucusu için.</span><span class="sxs-lookup"><span data-stu-id="20202-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="20202-151">4 adımda 2 izleyin **MySQL sunucusu için bir Azure veritabanı oluşturma** toochange işlem birimlerinde hello aynı fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="20202-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="20202-152">MySQL sunucusu için bir Azure veritabanını silin</span><span class="sxs-lookup"><span data-stu-id="20202-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="20202-153">1 - sunucuda hello **genel bakış** dikey penceresinde tıklatın **silmek** komut düğmesi tooopen hello silme onayı dikey.</span><span class="sxs-lookup"><span data-stu-id="20202-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="20202-154">Giriş kutusuna çift onay hello dikey 2-type hello doğru sunucu adı.</span><span class="sxs-lookup"><span data-stu-id="20202-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="20202-155">3-tıklatın **silmek** yeniden eylem silme tooconfirm düğmesine tıklayın ve açılan için "başarı silme" Merhaba bildirim çubuğunda bekleyin.</span><span class="sxs-lookup"><span data-stu-id="20202-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="20202-156">MySQL veritabanları için liste hello Azure veritabanı</span><span class="sxs-lookup"><span data-stu-id="20202-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="20202-157">Merhaba sunucuda **genel bakış** dikey penceresinde hello veritabanı görene kadar aşağı kaydırın döşeme hello alta.</span><span class="sxs-lookup"><span data-stu-id="20202-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="20202-158">Tüm hello veritabanları hello tabloda listelenir.</span><span class="sxs-lookup"><span data-stu-id="20202-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="20202-159">tıklatın **silmek** komut düğmesi tooopen hello silme onayı dikey.</span><span class="sxs-lookup"><span data-stu-id="20202-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![Veritabanlarını göster](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="20202-161">MySQL sunucusu için bir Azure veritabanının ayrıntılarını göster</span><span class="sxs-lookup"><span data-stu-id="20202-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="20202-162">Tıklatın **özellikleri** altında **ayarları** hello sunucuda hello dikey pencere açılır **özellikleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="20202-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="20202-163">Ardından, hello sunucu tüm ayrıntılı bilgileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20202-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20202-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20202-164">Next steps</span></span>

[<span data-ttu-id="20202-165">Hızlı Başlangıç: Azure veritabanı için Azure portalını kullanarak MySQL sunucusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20202-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
