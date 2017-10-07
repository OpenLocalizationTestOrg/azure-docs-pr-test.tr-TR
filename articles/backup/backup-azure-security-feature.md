---
title: "aaaSecurity özellikleri toohelp korumak Azure Yedekleme'yi karma yedeklemeleri | Microsoft Docs"
description: "Nasıl daha güvenli Azure Backup toomake yedeklere toouse güvenlik özelliklerini öğrenin"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pajosh
ms.openlocfilehash: 17a0f5e877f84af53c15062ec4a8df480383125e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-features-toohelp-protect-hybrid-backups-that-use-azure-backup"></a>Güvenlik özellikleri toohelp korumak Azure Yedekleme'yi karma yedekleri
Kötü amaçlı yazılım, yazılımı ve yetkisiz erişim, gibi güvenlik sorunları hakkında endişeleriniz artmaktadır. Bu güvenlik sorunları para ve veri açısından pahalı olabilir. Azure Backup şimdi bu tür saldırılara karşı tooguard sağlayan güvenlik özellikleri toohelp korumak karma yedeklemeler. Bu makalede, nasıl tooenable ve kullanım bu özellik, bir Azure kurtarma Hizmetleri aracısını ve Azure yedekleme Sunucusu'nu kullanarak yer almaktadır. Bu özellikler şunlardır:

- **Önleme**. Bir parola değiştirme gibi kritik bir işlem gerçekleştirildiğinde ek bir kimlik doğrulama katmanı eklenir. Bu doğrulama gibi işlemleri olabilir tooensure olan geçerli Azure kimlik bilgilerine sahip kullanıcılar tarafından gerçekleştirilen.
- **Uyarı**. Toohello Abonelik Yöneticisi Yedekleme verileri silme gibi kritik bir işlem olduğunda gerçekleştirilen bir e-posta bildirimi gönderilir. Bu e-posta hello kullanıcı hızla gibi eylemleri hakkında bildirim sağlar.
- **Kurtarma**. Silinen yedekleme verilerini hello silme hello tarihinden itibaren 14 gün için ek bir korunur. Bu yüzden hiçbir veri kaybı saldırının olsa bile bu belirli bir süre içinde kurtarılabilirliği hello veri sağlar. Ayrıca, en az kurtarma noktası daha fazla sayıda tooguard bozuk veri karşı korunur.

> [!NOTE]
> Altyapı (ıaas) VM yedekleme olarak kullanıyorsanız, güvenlik özellikleri etkinleştirilmemelidir. Bu özellikler etkinleştirmeden etkilerini kalmaması henüz Iaas VM yedekleme için kullanılabilir değildir. Yalnızca kullanıyorsanız, güvenlik özellikleri etkinleştirilmiş olmalıdır: <br/>
>  * **Azure Backup Aracısı**. En düşük aracı sürümü 2.0.9052. Bu özellikler etkinleştirdikten sonra toothis Aracı sürüm tooperform kritik işlemleri yükseltmeniz gerekir. <br/>
>  * **Azure Backup sunucusu**. En düşük Azure Yedekleme aracısı sürümü 2.0.9052 Azure yedekleme sunucusu ile güncelleştirme 1. <br/>
>  * **System Center Data Protection Manager**. En düşük Azure Yedekleme aracısı sürümü 2.0.9052 Data Protection Manager 2012 R2 UR12 veya Data Protection Manager 2016 UR2. <br/> 


> [!NOTE]
> Bu özellikler, yalnızca kurtarma Hizmetleri kasası için kullanılabilir. Kurtarma Hizmetleri kasalarının yeni oluşturulan tüm hello varsayılan olarak etkinleştirilen bu özellikler vardır. Var olan kurtarma Hizmetleri kasalarının kullanıcılar bu özellikler bölümü aşağıdaki hello bahsedilen hello adımları kullanarak etkinleştirin. Özelliklerinin etkin olduğu hello sonra bunlar tooall hello kurtarma Hizmetleri Aracısı Bilgisayarları, Azure yedekleme sunucusu örnekleri ve Data Protection Manager sunucuları hello kasasına kayıtlı geçerlidir. Bu ayarın etkinleştirilmesi tek seferlik bir işlemdir ve etkinleştirdikten sonra bu özellikleri devre dışı bırakılamıyor.
>

## <a name="enable-security-features"></a>Güvenlik özellikleri sağlar
Kurtarma Hizmetleri kasası oluşturuyorsanız, tüm hello güvenlik özelliklerini kullanabilirsiniz. Varolan bir kasa ile çalışıyorsanız, aşağıdaki adımları izleyerek güvenlik özellikleri sağlar:

1. Toohello Azure portal, Azure kimlik bilgilerinizi kullanarak oturum açın.
2. Seçin **Gözat**ve türü **kurtarma Hizmetleri**.

    ![Ekran görüntüsü, Azure portal gözatma seçeneği](./media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    Kurtarma Hizmetleri kasaları Hello listesi görüntülenir. Bu listeden bir kasa seçin. Merhaba seçilen kasa panosu açılır.
3. Listeden hello kasasında altında görüntülenen hello öğelerinin **ayarları**, tıklatın **özellikleri**.

    ![Ekran görüntüsü, Kurtarma Hizmetleri kasası seçenekleri](./media/backup-azure-security-feature/vault-list-properties.png)
4. Altında **güvenlik ayarları**, tıklatın **güncelleştirme**.

    ![Ekran görüntüsü, Kurtarma Hizmetleri kasası özellikleri](./media/backup-azure-security-feature/security-settings-update.png)

    Merhaba güncelleştirme bağlantı açar hello **güvenlik ayarları** hello özelliklerinin bir özetini sağlar ve bunları sağlamanıza olanak tanır, dikey.
5. Merhaba aşağı açılan listeden **Azure multi-Factor Authentication yapılandırdığınız?**, etkinleştirdiyseniz değeri tooconfirm seçin [Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md). Etkinleştirilirse, toohello Azure portal imzalarken tooauthenticate başka bir CİHAZDAN (örneğin, cep telefonu) istenir.

   Yedekleme kritik işlemler gerçekleştirdiğinizde, PIN, Azure portal hello üzerinde kullanılabilir güvenlik tooenter vardır. Azure multi-Factor Authentication etkinleştirilmesi bir güvenlik katmanı ekler. Yalnızca yetkili kullanıcıların geçerli Azure kimlik bilgileriyle ve ikinci bir CİHAZDAN kimlik doğrulaması hello Azure portalına erişebilir.
6. toosave güvenlik ayarlarını seçin **etkinleştirmek** tıklatıp **kaydetmek**. Seçebileceğiniz **etkinleştirmek** yalnızca hello bir değer seçtikten sonra **Azure multi-Factor Authentication yapılandırdığınız?** hello önceki adımda listesi.

    ![Güvenlik ayarları ekran görüntüsü](./media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a>Yedekleme verileri Kurtar silindi
Yedekleme ek 14 gün boyunca silinen yedekleme verilerini korur ve onu hemen hello varsa silmez **Dur yedekleme yedekleme verileri silmek ile** işlemi gerçekleştirilir. kullanmakta olduğunuz bağlı olarak, adımlara hello toorestore hello 14 günlük süre içinde bu verileri alın:

İçin **Azure kurtarma Hizmetleri aracısını** kullanıcılar:

1. Hello bilgisayar yedekler nerede gerçekleştiği hala kullanılabilir durumdaysa kullanmak [kurtarmak veri toohello aynı makine](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) Azure kurtarma Hizmetleri toorecover tüm hello eski kurtarma noktalarına ait.
2. Bu bilgisayarda kullanılabilir durumda değilse, kullanın [kurtarma tooan alternatif makine](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) toouse başka bir Azure kurtarma hizmetleri bilgisayar tooget bu verileri.

İçin **Azure yedekleme sunucusu** kullanıcılar:

1. Hello sunucusu yedekler nerede gerçekleştiği hala kullanılabilir ise, silinen hello veri kaynaklarını yeniden korumak ve hello kullan **verileri kurtarabilirsiniz** toorecover tüm hello eski kurtarma noktalarına ait özellik.
2. Bu sunucu kullanılabilir değilse, [başka bir Azure yedekleme sunucusundan veri Kurtar](backup-azure-alternate-dpm-server.md) toouse başka bir Azure yedekleme sunucusu örneği tooget bu verileri.

İçin **Data Protection Manager** kullanıcılar:

1. Hello sunucusu yedekler nerede gerçekleştiği hala kullanılabilir ise, silinen hello veri kaynaklarını yeniden korumak ve hello kullan **verileri kurtarabilirsiniz** toorecover tüm hello eski kurtarma noktalarına ait özellik.
2. Bu sunucu kullanılabilir değilse, [dış DPM Ekle](backup-azure-alternate-dpm-server.md) toouse başka bir Data Protection Manager sunucu tooget bu verileri.

## <a name="prevent-attacks"></a>Saldırıları önlemek
Denetimleri yalnızca geçerli kullanıcıların çeşitli işlemler gerçekleştirebilirsiniz emin toomake eklenmiştir. Bunlar, fazladan bir kimlik doğrulama katmanı ekleme ve kurtarma amacıyla bir minimum bekletme aralığı koruyarak içerir.

### <a name="authentication-tooperform-critical-operations"></a>Kimlik doğrulama tooperform kritik işlemler
Kimlik doğrulaması kritik işlemler için fazladan bir katmanı eklemenin bir parçası olarak, gerçekleştirdiğinizde istendiğinde tooenter güvenlik PIN olan **Delete verilerle korumayı Durdur** ve **değişiklik parola** işlemleri .

tooreceive Bu PIN:

1. Toohello Azure portalında oturum açın.
2. Çok Gözat**kurtarma Hizmetleri kasası** > **ayarları** > **özellikleri**.
3. Altında **güvenlik PIN**, tıklatın **Generate**. Hello Azure kurtarma Hizmetleri Aracısı kullanıcı arabiriminde girilen hello PIN toobe içeren dikey pencere açılır.
    Bu PIN yalnızca beş dakika için geçerlidir ve bu süreden sonra otomatik olarak oluşturulan.

### <a name="maintain-a-minimum-retention-range"></a>Minimum bekletme aralığı koru
kullanılabilir tooensure olmadığını her zaman geçerli bir sayı kurtarma noktaları, denetimleri aşağıdaki hello eklenmiştir:

- Günlük bekletme, en az **yedi** gün bekletme yapılması.
- Haftalık bekletme, en az **dört** hafta bekletme yapılması.
- Aylık bekletme, en az **üç** aylık saklamayla yapılması.
- Yıllık bekletme, en az **bir** bekletme yılın yapılması.

## <a name="notifications-for-critical-operations"></a>Bildirimleri kritik işlemleri için
Genellikle, kritik bir işlem gerçekleştirilirken hello Abonelik Yöneticisi hello işlemi hakkında ayrıntıları içeren bir e-posta bildirimi gönderilir. Bu bildirimler için ek e-posta alıcıları hello Azure portal kullanarak yapılandırabilirsiniz.

Bu makalede açıklanan hello güvenlik özellikleri hedeflenen saldırılara karşı savunma mekanizmaları sağlar. Saldırının oluşursa, daha da önemlisi, bu özellikler size özelliği toorecover verilerinizi hello.

## <a name="troubleshooting-errors"></a>Sorun giderme
| İşlem | Hata ayrıntıları | Çözüm |
| --- | --- | --- |
| İlke değişikliği |Merhaba yedekleme İlkesi değiştirilemedi. Hata: tooan iç hizmet hatası [0x29834] hello geçerli işlem başarısız oldu. Lütfen hello işlemi bir süre sonra yeniden deneyin. Merhaba sorun devam ederse, lütfen Microsoft Destek'e başvurun. |**Neden:**<br/>Bu hata güvenlik ayarlarını etkin, yukarıda belirtilen minimum değerler hello aşağıda tooreduce bekletme aralığı deneyin ve desteklenmeyen sürümü gelir (desteklenen sürümleri, bu makalenin ilk notta belirtilir). <br/>**Önerilen eylem:**<br/> Bu durumda, yukarıda belirtilen dönem hello minimum bekletme (günlük, haftalık, üç hafta aylık veya yıllık yedekleme için bir yıl için dört hafta için yedi gün) saklama dönemi ayarlamalısınız tooproceed ilkesiyle ilgili güncelleştirdi. İsteğe bağlı olarak, tercih edilen yaklaşım tooupdate yedekleme aracısını olacaktır, Azure yedekleme sunucusu ve/veya DPM UR tooleverage tüm hello güvenlik güncelleştirir. |
| Parola değiştirme |Güvenlik girdiğiniz PIN yanlış. (KİMLİK: 100130) Bu işlem Hello doğru güvenlik PIN toocomplete sağlar. |**Neden:**<br/> (Parola değiştirme gibi) kritik işlemi gerçekleştirirken geçersiz veya süresi dolmuş güvenlik PIN girdiğinizde, bu hata verilir. <br/>**Önerilen eylem:**<br/> toocomplete hello işlemi, geçerli güvenlik PIN girmeniz gerekir. tooget PIN Merhaba, tooAzure Portalı'nda oturum açın ve tooRecovery Hizmetleri kasasına gidin > Ayarlar > Özellikler > Güvenlik PIN oluşturun. Bu PIN toochange parolayı kullanın. |
| Parola değiştirme |İşlem başarısız oldu. KİMLİĞİ: 120002 |**Neden:**<br/>Bu hata, güvenlik ayarları etkin, toochange parolayı deneyin ve desteklenmeyen sürümüne (geçerli sürümleri, bu makalenin ilk notta belirtilen) gelir.<br/>**Önerilen eylem:**<br/> toochange parola, Yedekleme aracısı toominimum sürümü en düşük 2.0.9052, Azure yedekleme sunucusu toominimum güncelleştirme 1 ve/veya DPM 2012 R2 UR12 veya DPM 2016 geçerli güvenlik PIN girme UR2 (indirme aşağıdaki bağlantıları), DPM toominimum önce güncelleştirmeniz gerekir. tooget PIN Merhaba, tooAzure Portalı'nda oturum açın ve tooRecovery Hizmetleri kasasına gidin > Ayarlar > Özellikler > Güvenlik PIN oluşturun. Bu PIN toochange parolayı kullanın. |

## <a name="next-steps"></a>Sonraki adımlar
* [Azure kurtarma Hizmetleri kasası ile çalışmaya başlama](backup-azure-vms-first-look-arm.md) tooenable bu özellikleri.
* [Merhaba en son Azure kurtarma Hizmetleri Aracısı'nı indirme](http://aka.ms/azurebackup_agent) toohelp Windows bilgisayarların korunmasına ve yedekleme verilerinizi saldırılara karşı koruma.
* [İndirme hello en son Azure yedekleme sunucusu](https://aka.ms/latest_azurebackupserver) toohelp iş yüklerini korumak ve yedekleme verilerinizi saldırılara karşı koruma.
* [System Center 2012 R2 Data Protection Manager için UR12 karşıdan](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) veya [UR2 System Center 2016 Data Protection Manager için karşıdan](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) toohelp iş yüklerini korumak ve yedekleme verilerinizi saldırılara karşı koruma.
