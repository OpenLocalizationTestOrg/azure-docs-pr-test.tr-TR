---
title: "Exchange server tooAzure System Center 2012 R2 DPM yedeklemesiyle yukarı aaaBack | Microsoft Docs"
description: "Bilgi nasıl tooback bir Exchange server tooAzure yukarı yedekleme System Center 2012 R2 DPM kullanma"
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a>Exchange server tooAzure System Center 2012 R2 DPM yedeklemesiyle yedekleyin
Bu makalede nasıl tooconfigure System Center 2012 R2 Data Protection Manager (DPM) sunucu tooback bir Microsoft Exchange sunucusu çok Azure yedekleme.  

## <a name="updates"></a>Güncelleştirmeler
toosuccessfully kayıt hello DPM sunucusu Azure yedekleme ile hello Azure Yedekleme aracısı System Center 2012 R2 DPM ve hello en son sürümü için en son güncelleştirme toplaması hello yüklemeniz gerekir. Hello Hello en son güncelleştirme paketi Al [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).

> [!NOTE]
> Bu makaledeki örneklerde Merhaba, hello Azure yedekleme Aracısı'nın 2.0.8719.0 sürümü yüklü ve güncelleştirme paketi 6 System Center 2012 R2 DPM üzerinde yüklü.
>
>

## <a name="prerequisites"></a>Ön koşullar
Devam etmeden önce tüm hello emin olun [Önkoşullar](backup-azure-dpm-introduction.md#prerequisites) tooprotect iş yükleri için Microsoft Azure Yedekleme kullanılarak karşılandığından. Bu Önkoşullar hello şunları içerir:

* Bir yedekleme kasası hello Azure site üzerinde oluşturuldu.
* Aracısını ve kasa kimlik bilgileri indirilen toohello DPM sunucusunun silinmiş.
* Merhaba Aracısı hello DPM sunucusuna yüklenir.
* Merhaba kasa kimlik bilgileri kullanılan tooregister hello DPM sunucusu yoktu.
* Lütfen Exchange 2016 koruyorsanız, tooDPM 2012 R2 UR9 yükseltme yapın veya daha yenisi

## <a name="dpm-protection-agent"></a>DPM koruma Aracısı
tooinstall hello DPM koruma Aracısı hello Exchange sunucusunda şu adımları izleyin:

1. Merhaba güvenlik duvarları doğru şekilde yapılandırıldığından emin olun. Bkz: [hello aracı için güvenlik duvarı özel durumlarını yapılandırma](https://technet.microsoft.com/library/Hh758204.aspx).
2. Tıklayarak hello Exchange sunucusunda Hello aracı yükleme **Yönetim > aracıları > yükleme** DPM yönetici Konsolu'ndaki. Bkz: [yükleme hello DPM koruma Aracısı](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) ayrıntılı adımlar için.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Merhaba Exchange sunucusu için bir koruma grubu oluşturma
1. Hello DPM Yönetici Konsolu, tıklatın **koruma**ve ardından **yeni** hello aracı Şerit tooopen hello üzerinde **yeni koruma grubu oluşturma** Sihirbazı.
2. Merhaba üzerinde **Hoş Geldiniz** hello Sihirbazı'nı ekranın **sonraki**.
3. Merhaba üzerinde **koruma grubu türünü seçin** ekranında, seçin **sunucuları** tıklatıp **sonraki**.
4. Select hello Exchange server veritabanına tooprotect istediğiniz ve tıklayın **sonraki**.

   > [!NOTE]
   > Exchange 2013 koruyorsanız hello denetleyin [Exchange 2013 önkoşulları](https://technet.microsoft.com/library/dn751029.aspx).
   >
   >

    Aşağıdaki örneğine hello hello Exchange 2010 veritabanı seçilir.

    ![Grup üyelerini seçin](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Merhaba veri koruma yöntemini seçin.

    Merhaba koruma grubu adı ve aşağıdaki seçenekleri şu hello her ikisini de seçin:

   * Disk kullanılan kısa vadeli koruma istiyorum.
   * Çevrimiçi koruma istiyorum.
6. **İleri**’ye tıklayın.
7. Select hello **Eseutil'i Çalıştır toocheck veri bütünlüğü** toocheck hello hello Exchange Server veritabanlarının bütünlüğünü istiyorsanız seçeneği.

    Bu seçeneği belirledikten sonra yedekleme tutarlılığı denetleniyor hello çalıştırarak hello DPM sunucusu tooavoid hello g/ç trafiği üzerinde çalıştırılacak **eseutil** hello Exchange sunucusundaki komutu.

   > [!NOTE]
   > toouse bu seçenek, hello Ese.dll ve Eseutil.exe dosyalarını toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin dizin hello DPM sunucusunda kopyalamanız gerekir. Aksi takdirde, aşağıdaki hata hello tetiklenir:  
   > ![Eseutil hata](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. **İleri**’ye tıklayın.
9. Select hello veritabanı için **kopya yedekleme**ve ardından **sonraki**.

   > [!NOTE]
   > Bir veritabanı en az bir DAG kopyası için "tam yedekleme" seçeneğini belirlemezseniz günlükler kesilmez.
   >
   >
10. Merhaba hedeflerini yapılandırma **kısa vadeli yedekleme**ve ardından **sonraki**.
11. Merhaba kullanılabilir disk alanını gözden geçirin ve ardından **sonraki**.
12. DPM hangi hello sunucu hello ilk çoğaltma oluşturur ve ardından başlangıç saati seçin **sonraki**.
13. Merhaba tutarlılık denetimi seçeneklerini seçin ve ardından **sonraki**.
14. Tooback tooAzure yedeklemek istediğiniz ve ardından hello veritabanı seçin **sonraki**. Örneğin:

    ![Çevrimiçi koruma verilerini belirtin](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. İçin Hello zamanlama tanımla **Azure Backup**ve ardından **sonraki**. Örneğin:

    ![Çevrimiçi Yedekleme zamanlamasını belirtin](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > Çevrimiçi kurtarma noktası hızlı temel unutmayın tam kurtarma noktaları. Bu nedenle, hello çevrimiçi kurtarma noktası zamanlama belirtilen hello süredir hello sonra tam kurtarma noktası express.
    >
    >
16. Merhaba bekletme ilkesi yapılandırma **Azure Backup**ve ardından **sonraki**.
17. Çevrimiçi çoğaltma seçeneğini belirleyin ve tıklatın **sonraki**.

    Büyük bir veritabanınız varsa, hello ilk yedekleme toobe hello ağ üzerinden oluşturulan uzun bir süredir ele geçirebilir. tooavoid bu sorunu çevrimdışı yedekleme oluşturabilirsiniz.  

    ![Çevrimiçi bekletme ilkesini belirtin](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Hello ayarlarını onaylayın ve ardından **Grup Oluştur**.
19. **Kapat**’a tıklayın.

## <a name="recover-hello-exchange-database"></a>Merhaba Exchange veritabanını kurtarma
1. bir Exchange veritabanı toorecover tıklatın **kurtarma** hello DPM Yönetici Konsolu içinde.
2. Toorecover istediğiniz hello Exchange veritabanını bulun.
3. Merhaba çevrimiçi bir kurtarma noktası seçin *kurtarma süresini* aşağı açılan liste.
4. Tıklatın **kurtarmak** toostart hello **Kurtarma Sihirbazı'nı**.

Çevrimiçi kurtarma noktaları için beş kurtarma türü vardır:

* **Toooriginal Exchange Server konumuna Kurtar:** hello veriler, kurtarılan toohello özgün Exchange server olacaktır.
* **Exchange Server üzerindeki tooanother veritabanını Kurtar:** hello veriler, kurtarılan tooanother veritabanı başka bir Exchange sunucusu üzerinde olacaktır.
* **Tooa kurtarma veritabanına Kurtar:** hello veriler, kurtarılan tooan Exchange kurtarma veritabanına (RDB) olacaktır.
* **Kopya tooa ağ klasörüne:** hello veriler, kurtarılan tooa ağ klasörüne olacaktır.
* **Tootape kopyalayın:** bir bant kitaplığınız veya ekli ve yapılandırılmış hello DPM sunucusu, hello kurtarma noktası olacaktır bir tek başına bant sürücüsünü tooa boş bant kopyalanır.

    ![Çevrimiçi çoğaltma seçin](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Backup ile ilgili SSS](backup-azure-backup-faq.md)
