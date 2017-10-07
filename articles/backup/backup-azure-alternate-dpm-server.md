---
title: bir Azure yedekleme sunucusu aaaRecover verilerden | Microsoft Docs
description: "Korunan hello verileri kurtarmak tooa kurtarma Hizmetleri kasası tüm Azure yedekleme sunucusu kayıtlı toothat kasadan."
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a>Azure Backup Sunucusu’ndan veri kurtarma
Azure yedekleme sunucusu toorecover hello veri kurtarma Hizmetleri kasası tooa yedeklediğinize göre kullanabilirsiniz. Merhaba işlem yapmak için bu nedenle hello Azure yedekleme sunucusu Yönetim Konsolu'na tümleştirilmiştir ve diğer Azure Backup bileşenleri için benzer toohello kurtarma iş akışı.

> [!NOTE]
> Bu makalede [System Center Data Protection Manager 2012 R2 için UR7 veya sonraki sürümleriyle] (https://support.microsoft.com/en-us/kb/3065246) geçerlidir hello ile birlikte [en son Azure Backup aracısını](http://aka.ms/azurebackup_agent).
>
>

bir Azure yedekleme sunucusu veri toorecover:

1. Hello gelen **kurtarma** hello Azure yedekleme sunucusu Yönetim Konsolu, sekmesini **'Dış DPM Ekle'** (hello adresindeki hello ekranın sol üst).   
    ![Dış DPM Ekle](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)
2. Yeni Yükleme **kasa kimlik bilgileri** hello ile ilişkili hello kasasından **Azure yedekleme sunucusu** hello veri kurtarılmakta olan yerlerde, hello Azure yedekleme sunucusu hello Azure yedekleme sunucuların listesinden seçin. Merhaba kurtarma Hizmetleri kasasına kayıtlı ve hello sağlamak **şifreleme parolası** verisini kurtarıldığı hello sunucusuyla ilişkilendirilmiş.

    ![Dış DPM kimlik bilgileri](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > Yalnızca Azure yedekleme sunucuları aynı hello ile ilişkilendirilen kayıt kasası birbirlerinin verileri kurtarabilir.
   >
   >

    Merhaba dış Azure yedekleme sunucusu başarıyla olduğunda eklenir, hello veri hello dış sunucunun göz atabilmeniz ve hello yerel Azure yedekleme sunucusundan hello **kurtarma** sekmesi.
3. Gözat hello kullanılabilir listesini üretim sunucuları tarafından korunan dış Azure yedekleme sunucusu hello ve hello uygun veri kaynağını seçin.

    ![Dış DPM sunucusu Gözat](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. Seçin **hello ay ve yıl** hello gelen **kurtarma noktaları** gerekli select hello aşağı bırakma **kurtarma tarih** zaman hello kurtarma noktası oluşturulduğundan ve select hello olduğu için **Kurtarma süresini**.

    Dosya ve klasörlerin listesini gözatılabilir ve tooany konumu kurtarılan hello alt bölmesinde görüntülenir.

    ![Dış DPM sunucusunu kurtarma noktaları](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. Merhaba uygun öğeyi sağ tıklatın ve'ı tıklatın **kurtarmak**.

    ![Dış DPM kurtarma](./media/backup-azure-alternate-dpm-server/recover.png)
6. Gözden geçirme hello **kurtarmak seçimi**. Merhaba veri ve kurtarılan hello yedeğini süresini yanı sıra, hello yedek kopya oluşturulduğu hello kaynak doğrulayın. Merhaba seçimi yanlışsa tıklatın **iptal** toonavigate geri toorecovery sekmesini tooselect uygun kurtarma noktası. Merhaba seçimi doğru ise, tıklatın **sonraki**.

    ![Dış DPM kurtarma özeti](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. Seçin **tooan alternatif konuma Kurtar**. **Gözat** toohello doğru konuma hello kurtarma.

    ![Dış DPM kurtarma alternatif konumu](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. Çok ilgili hello seçeneği**kopya oluştur**, **atla**, veya **üzerine yaz**.

   * **Kopya Oluştur** -bir ad çakışması ise hello dosyanın bir kopyasını oluşturur.
   * **Atla** - bir ad çakışması varsa hello özgün dosya bırakır hello dosya kurtarılmıyor.
   * **Üzerine** - bir ad çakışması varsa hello dosya hello kopyasının üzerine yazar.

     Merhaba uygun çok seçeneği**geri güvenlik**. Burada hello veri kurtarılacak hello hedef bilgisayarın güvenlik ayarlarını hello veya geçerli tooproduct hello kurtarma noktasının oluşturulduğu hello zamanki hello güvenlik ayarlarını uygulayabilirsiniz.

     Tanımlamak olup bir **bildirim** hello kurtarma başarıyla tamamlandıktan sonra gönderilir.

     ![Dış DPM kurtarma bildirimleri](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. Merhaba **Özet** ekran kadarki seçilen hello seçenekleri listeler. Tıkladığınızda **'Kurtar'**, hello verilerdir kurtarılan toohello uygun şirket içi konumu.

    ![Dış DPM kurtarma seçenekleri özeti](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > Merhaba kurtarma işi hello izlenebilir **izleme** hello Azure yedekleme sunucusu sekmesinde.
   >
   >

    ![Kurtarma izleme](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. Tıklayabilirsiniz **dış DPM Temizle** hello üzerinde **kurtarma** hello hello dış DPM sunucusunun DPM sunucu tooremove hello görünümü sekmesinde.

    ![Dış DPM Temizle](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a>Hata iletileri sorunlarını giderme
| Hayır. | Hata iletisi | Sorun giderme adımları |
|:---:|:--- |:--- |
| 1. |Bu sunucu hello kasa kimlik bilgileri tarafından belirtilen kasaya kayıtlı toohello değil. |**Neden:** bu hatayı seçili hello kasa kimlik bilgilerini ait olmayan kurtarma Hizmetleri kasası toohello ilişkili Azure yedekleme sunucusu hangi hello kurtarma denemesi görünür. <br> **Çözüm:** indirme hello kasa kimlik bilgilerini Azure yedekleme sunucusu kayıtlı hello kurtarma Hizmetleri kasası toowhich hello gelen. |
| 2. |Merhaba kurtarılabilir veriler kullanılamıyor veya hello seçili sunucu DPM sunucusu değil. |**Neden:** hiçbir diğer Azure yedekleme sunucuları kayıtlı toohello kurtarma Hizmetleri kasası, vardır veya hello sunucuları henüz karşıya hello meta verileri veya hello seçili sunucu bir Azure yedekleme sunucusu (diğer adıyla Windows Server veya Windows istemcisi) değil. <br> **Çözüm:** diğer Azure yedekleme sunucuları kayıtlı toohello kurtarma Hizmetleri kasası varsa, o hello en son Azure Backup aracısının yüklü olduğundan emin olun. <br>Diğer Azure yedekleme sunucuları kayıtlı toohello kurtarma Hizmetleri kasası varsa, yükleme toostart hello kurtarma işlemi sonraki bir gün bekleyin. Merhaba gecelik iş için tüm korumalı hello yedeklemeleri toocloud hello meta veriler karşıya yükler. Merhaba veri kurtarma için kullanılabilir. |
| 3. |Başka bir DPM sunucusu kayıtlı toothis Kasası ' dir. |**Neden:** diğer Azure yedekleme hangi hello kurtarma denemesi kayıtlı toohello kasası olan sunucu yok.<br>**Çözüm:** diğer Azure yedekleme sunucuları kayıtlı toohello kurtarma Hizmetleri kasası varsa, o hello en son Azure Backup aracısının yüklü olduğundan emin olun.<br>Diğer Azure yedekleme sunucuları kayıtlı toohello kurtarma Hizmetleri kasası varsa, yükleme toostart hello kurtarma işlemi sonraki bir gün bekleyin. Merhaba gecelik iş için tüm korumalı yedeklemeler toocloud hello meta verilerini karşıya yükleme. Merhaba veri kurtarma için kullanılabilir. |
| 4. |sağlanan şifreleme parolası hello sunucu hello ile ilişkili parolayla eşleşmiyor:**<server name>** |**Neden:** kurtarılacak hello Azure yedekleme sunucunun veri hello verileri şifreleme işleminin hello kullanılan hello şifreleme parolası sağlanan hello şifreleme parolası eşleşmiyor. Merhaba Aracısı yüklenemiyor toodecrypt hello verilerdir. Bu nedenle hello kurtarma başarısız olur.<br>**Çözüm:** Lütfen hello Azure yedekleme verileri kurtarıldığı sunucusu ile ilişkili hello tam aynı şifreleme parolası belirtin. |

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a>Harici bir DPM sunucusu UR7 ve en son Azure Backup aracısını yükledikten sonra neden ekleyemiyorum?

Merhaba DPM olan veri kaynakları ile toohello bulut (güncelleştirme paketi 7'den önceki, bir güncelleştirme paketi kullanarak) korumalı sunucuları için hello UR7 ve en son Azure Backup aracısını, toostart yükledikten sonra en az bir gün beklemeniz gerekir **dış DPM Ekle sunucu** . Merhaba bir günlük süre hello DPM koruma grupları tooAzure gerekli tooupload hello meta verileri ' dir. Koruma grubu meta veri yüklendiği hello gecelik işi üzerinden ilk kez.

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a>Merhaba hello Microsoft Azure kurtarma Hizmetleri Aracısı gerekli en düşük sürümü nedir?

Merhaba Microsoft Azure kurtarma Hizmetleri Aracısı ya da Azure Yedekleme aracısı, gerekli tooenable en düşük sürümü Hello 2.0.8719.0 bu özelliğidir.  tooview hello aracının sürümünü: Denetim Masası'nı açın  **>**  tüm Denetim Masası öğeleri  **>**  programlar ve Özellikler  **>**  Microsoft Azure kurtarma Hizmetleri Aracısı. Merhaba sürümü 2.0.8719.0'den az ise, yükleyip hello [en son Azure Backup aracısını](https://go.microsoft.com/fwLink/?LinkID=288905).

![Dış DPM Temizle](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a>Sonraki adımlar:
• [Azure Backup ile ilgili SSS](backup-azure-backup-faq.md)
