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
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Oluşturma ve Azure veritabanı MySQL sunucusu için Azure portalını kullanarak yönetme
Bu makalede nasıl hızlı bir şekilde MySQL sunucusu için yeni bir Azure veritabanı oluşturabilir ve hello sunucuyu hello Azure Portal kullanarak yönetiyorsanız açıklanmaktadır. Sunucu Yönetimi Sunucusu ayrıntılarını & veritabanları görüntüleme, parola sıfırlama ve hello sunucuyu silmek içerir.

## <a name="log-in-toohello-azure-portal"></a>Toohello Azure portalında oturum açın
İçinde toohello oturum [Azure portal](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>MySQL için Azure Veritabanı sunucusu oluşturma
Bu adımları toocreate "mysqlserver4demo" adlı MySQL sunucusu için bir Azure veritabanı izleyin

1-tıklatma **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.

2-seçin **veritabanları** hello yeni sayfa ve select **Azure veritabanı için MySQL** hello veritabanları sayfasından.

> MySQL sunucusu için bir Azure veritabanı tanımlanan bir dizi ile oluşturulan [işlem ve depolama](./concepts-compute-unit-and-storage.md) kaynakları. Merhaba veritabanı, MySQL sunucusu için bir Azure veritabanında, bir Azure kaynak grubu içinde oluşturulur.

![Yeni-sunucusu oluştur](./media/howto-create-manage-server-portal/create-new-server.png)

3 - hello Azure veritabanı MySQL form için aşağıdaki bilgilerle hello ile doldurun:

| **Form Alanı** | **Alan Açıklaması** |
|----------------|-----------------------|
| *Sunucu adı* | Azure mysql (sunucu adı genel olarak benzersiz) |
| *Abonelik* | MySQLaaS (açılan seçin) |
| *Kaynak grubu* | myresource (yeni bir kaynak grubu oluşturun veya var olanı kullanırsınız) |
| *Sunucu yöneticisi oturum açma bilgileri* | myadmin (yönetici hesabı adını ayarlayın) |
| *Parola* | Kurulum yönetici hesabı parolası |
| *Parolayı onayla* | yönetici hesabı parolasını onaylayın |
| *Konum* | Kuzey Avrupa (Kuzey Avrupa ve Batı ABD arasında seçim) |
| *Sürüm* | 5.6 (Azure veritabanı için MySQL sunucusu sürümü seçin) |

4-tıklatın **fiyatlandırma katmanı** toospecify hello Hizmet katmanını ve performans düzeyini yeni sunucunuzu. İşlem birim 50 ile temel katman, 100 ve 200 standart katmanındaki ile 100 arasında yapılandırılabilir ve depolama dahil edilen miktar bağlı olarak eklenebilir. Bu nasıl yapılır kılavuzu için şimdi bir 50 işlem birimi ve 50 GB'ı seçin. Tıklatın **Tamam** toosave seçiminizi.
![oluşturma sunucu-fiyatlandırma-katmanı](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

5'i tıklatın **oluşturma** tooprovision hello sunucu. Sağlama birkaç dakika sürer.

> Merhaba denetleyin **PIN toodashboard** seçeneği tooallow kolay izlenmesini dağıtımlarınızı.
> [!NOTE]
> Temel katmanındaki too1000GB ve 10000 GB standart katmanı depolama için genel Önizleme için desteklenecek hello maksimum depolama hala sınırlı too1000GB geçici olarak olsa. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>MySQL sunucusu için bir Azure veritabanını güncelleştirme
Yeni Sunucu sağlandıktan sonra kullanıcı 2 seçenekleri tooedit varolan sunucusu vardır.: sıfırlama yönetici parolası veya ölçek yukarı/aşağı hello sunucu hello işlem-birimleri değiştirerek.

### <a name="change-hello-administrator-user-password"></a>Hello Yöneticisi kullanıcı parolasını değiştirme
1 - sunucuda hello **genel bakış** dikey penceresinde tıklatın **parola sıfırlama** toopopulate bir parola giriş ve onay penceresi.

2 - yeni bir parola girin ve aşağıdaki şekilde hello penceresinde hello parolayı onaylayın: ![parola sıfırlama](./media/howto-create-manage-server-portal/reset-password.png)

3-tıklatın **Tamam** toosave hello yeni parola.

### <a name="scale-updown-by-changing-compute-units"></a>Ölçek yukarı/aşağı işlem birimleri değiştirerek

1 - üzerinde hello sunucu dikey altında **ayarları**, tıklatın **fiyatlandırma katmanı** tooopen hello fiyatlandırma katmanı dikey hello Azure veritabanı MySQL sunucusu için.

4 adımda 2 izleyin **MySQL sunucusu için bir Azure veritabanı oluşturma** toochange işlem birimlerinde hello aynı fiyatlandırma katmanı.

## <a name="delete-an-azure-database-for-mysql-server"></a>MySQL sunucusu için bir Azure veritabanını silin

1 - sunucuda hello **genel bakış** dikey penceresinde tıklatın **silmek** komut düğmesi tooopen hello silme onayı dikey.

Giriş kutusuna çift onay hello dikey 2-type hello doğru sunucu adı.

3-tıklatın **silmek** yeniden eylem silme tooconfirm düğmesine tıklayın ve açılan için "başarı silme" Merhaba bildirim çubuğunda bekleyin.

## <a name="list-hello-azure-database-for-mysql-databases"></a>MySQL veritabanları için liste hello Azure veritabanı
Merhaba sunucuda **genel bakış** dikey penceresinde hello veritabanı görene kadar aşağı kaydırın döşeme hello alta. Tüm hello veritabanları hello tabloda listelenir. tıklatın **silmek** komut düğmesi tooopen hello silme onayı dikey.

![Veritabanlarını göster](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>MySQL sunucusu için bir Azure veritabanının ayrıntılarını göster
Tıklatın **özellikleri** altında **ayarları** hello sunucuda hello dikey pencere açılır **özellikleri** dikey. Ardından, hello sunucu tüm ayrıntılı bilgileri görüntüleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

[Hızlı Başlangıç: Azure veritabanı için Azure portalını kullanarak MySQL sunucusu oluşturun.](./quickstart-create-mysql-server-database-using-azure-portal.md)
