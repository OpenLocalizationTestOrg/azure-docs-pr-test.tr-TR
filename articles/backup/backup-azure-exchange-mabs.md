---
title: Exchange server tooAzure yedekleme Azure yedekleme sunucusu ile ayarlama aaaBack | Microsoft Docs
description: "Bilgi nasıl tooback bir Exchange server tooAzure yukarı yedekleme Azure yedekleme sunucusu kullanarak"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a>Exchange server tooAzure yedekleme Azure yedekleme sunucusu ile yedekleyin
Bu makalede nasıl tooconfigure Microsoft Azure yedekleme sunucusu (MABS) tooback bir Microsoft Exchange server tooAzure ayarlama.  

## <a name="prerequisites"></a>Ön koşullar
Devam etmeden önce Azure yedekleme sunucusu olduğundan emin olun [yüklü ve hazırlanan](backup-azure-microsoft-azure-backup.md).

## <a name="mabs-protection-agent"></a>MABS koruma Aracısı
tooinstall hello MABS koruma Aracısı hello Exchange sunucusunda şu adımları izleyin:

1. Merhaba güvenlik duvarları doğru şekilde yapılandırıldığından emin olun. Bkz: [hello aracı için güvenlik duvarı özel durumlarını yapılandırma](https://technet.microsoft.com/library/Hh758204.aspx).
2. Tıklayarak hello Exchange sunucusunda Hello aracı yükleme **Yönetim > aracıları > yükleme** MABS Yönetici konsolunda. Bkz: [yükleme hello MABS koruma Aracısı](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) ayrıntılı adımlar için.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Merhaba Exchange sunucusu için bir koruma grubu oluşturma
1. Hello MABS Yönetici Konsolu, tıklatın **koruma**ve ardından **yeni** hello aracı Şerit tooopen hello üzerinde **yeni koruma grubu oluşturma** Sihirbazı.
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

    Bu seçeneği belirledikten sonra yedekleme tutarlılığı denetleniyor hello çalıştırarak oluşturulan MABS tooavoid hello g/ç trafiği üzerinde çalıştırılacak **eseutil** hello Exchange sunucusundaki komutu.

   > [!NOTE]
   > toouse bu seçenek, hello Ese.dll ve Eseutil.exe dosyalarını toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin hello MAB sunucusunda dizinine kopyalamanız gerekir. Aksi takdirde, aşağıdaki hata hello tetiklenir:  
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
12. Hangi hello MAB sunucu hello ilk çoğaltma oluşturur ve ardından başlangıç saati seçin **sonraki**.
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
1. bir Exchange veritabanı toorecover tıklatın **kurtarma** hello MABS Yönetici Konsolu içinde.
2. Toorecover istediğiniz hello Exchange veritabanını bulun.
3. Merhaba çevrimiçi bir kurtarma noktası seçin *kurtarma süresini* aşağı açılan liste.
4. Tıklatın **kurtarmak** toostart hello **Kurtarma Sihirbazı'nı**.

Çevrimiçi kurtarma noktaları için beş kurtarma türü vardır:

* **Toooriginal Exchange Server konumuna Kurtar:** hello veriler, kurtarılan toohello özgün Exchange server olacaktır.
* **Exchange Server üzerindeki tooanother veritabanını Kurtar:** hello veriler, kurtarılan tooanother veritabanı başka bir Exchange sunucusu üzerinde olacaktır.
* **Tooa kurtarma veritabanına Kurtar:** hello veriler, kurtarılan tooan Exchange kurtarma veritabanına (RDB) olacaktır.
* **Kopya tooa ağ klasörüne:** hello veriler, kurtarılan tooa ağ klasörüne olacaktır.
* **Tootape kopyalayın:** bir bant kitaplığınız veya ekli ve yapılandırılmış MABS, hello kurtarma noktası olacaktır bir tek başına bant sürücüsünü tooa boş bant kopyalanır.

    ![Çevrimiçi çoğaltma seçin](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Backup ile ilgili SSS](backup-azure-backup-faq.md)
