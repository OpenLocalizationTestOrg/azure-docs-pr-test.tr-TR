---
title: "Azure AD Connect: Toorecover LocalDB 10GB'den nasıl sınırlamak sorunu | Microsoft Docs"
description: "Bu konu, nasıl toorecover Azure AD Connect eşitleme hizmeti LocalDB 10 GB karşılaştığında açıklar sınırlamak sorun."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Azure AD Connect: Nasıl toorecover LocalDB 10 GB sınırını gelen
Azure AD Connect bir SQL Server veritabanı toostore kimlik verilerini gerektirir. Merhaba varsayılan olarak Azure AD Connect ile SQL Server 2012 Express LocalDB yüklenen kullanabilir veya kendi tam SQL kullanın. SQL Server Express 10 GB boyut sınırını uygular. LocalDB’yi kullanırken bu sınıra ulaşıldığında, Azure AD Connect Eşitleme Hizmeti artık düzgün başlatılamaz veya eşitleme yapamaz. Bu makalede hello kurtarma adımları sağlar.

## <a name="symptoms"></a>Belirtiler
İki ortak Belirtiler şunlardır:

* Azure AD Connect eşitleme hizmeti **çalıştıran** ancak toosynchronize ile başarısız *"durduruldu-veritabanı-disk dolu"* hata.

* Azure AD Connect eşitleme hizmeti **oluşturulamıyor toostart olan**. Toostart hello hizmet denediğinizde, olay 6323 ve hata iletisi ile başarısız *"Merhaba sunucu bir hatayla karşılaştı SQL sunucusu disk alanı yetersiz olduğundan."*

## <a name="short-term-recovery-steps"></a>Kısa vadeli kurtarma adımları
Bu bölüm, Azure AD Connect eşitleme hizmeti tooresume işlemi için gereken hello adımları tooreclaim DB alanı sağlar. Merhaba adımları içerir:
1. [Merhaba eşitleme hizmeti durumunu belirleme](#determine-the-synchronization-service-status)
2. [Merhaba veritabanı Daralt](#shrink-the-database)
3. [Geçmiş verileri çalışmasını sil](#delete-run-history-data)
4. [Çalıştırma geçmişi veri saklama süresini kısaltmak](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>Merhaba eşitleme hizmeti durumunu belirleme
İlk olarak, hello eşitleme hizmeti veya hala çalışıp çalışmadığını belirleyin:

1. Tooyour içinde Azure AD Connect sunucusu yönetici olarak oturum.

2. Çok Git**Hizmet Denetim Yöneticisi**.

3. Merhaba durumunu denetleme **Microsoft Azure AD eşitleme**.


4. Çalışıyorsa, etmeyin durdurmak veya hello hizmetini yeniden başlatın. Atla [küçültme hello veritabanı](#shrink-the-database) adım ve çok Git[Sil'i çalıştırmak geçmiş verileri](#delete-run-history-data) adım.

5. Toostart hello hizmeti çalışmıyorsa, deneyin. Merhaba hizmeti başarıyla başlatılırsa atla [küçültme hello veritabanı](#shrink-the-database) adım ve çok Git[Sil'i çalıştırmak geçmiş verileri](#delete-run-history-data) adım. Aksi takdirde devam [küçültme hello veritabanı](#shrink-the-database) adım.

### <a name="shrink-hello-database"></a>Merhaba veritabanı Daralt
Merhaba küçültme işlemi toofree yeterli DB alanı toostart hello eşitleme hizmeti yukarı kullanın. Bu, DB alanı hello veritabanında boşluk kaldırarak boşaltır. Bu adım en yüksek çaba aynıdır, alan her zaman kurtarabilirsiniz garanti edilmez. Küçültme işlemi hakkında daha fazla toolearn bu makalesini okuyun [bir veritabanını küçültmek](https://msdn.microsoft.com/library/ms189035.aspx).

> [!IMPORTANT]
> Merhaba eşitleme hizmeti toorun alırsanız, bu adımı atlayın. Toopoor performans tooincreased parçalanması nedeniyle açabilir gibi tooshrink hello SQL DB önerilmez.

Azure AD Connect için oluşturulan hello veritabanının Hello adı **ADSync**. tooperform küçültme işlemi, hello sysadmin ya da hello veritabanı DBO olarak oturum açmalısınız. Azure AD Connect yüklemesi sırasında hesapları aşağıdaki hello sysadmin hakları verilir:
* Yerel Yöneticiler
* kullanılan toorun Azure AD Connect yüklemesinin hello kullanıcı hesabı.
* Hello Azure AD Connect eşitleme hizmeti bağlamında işletim hello kullanılan eşitleme hizmeti hesabı.
* Merhaba yerel grup yükleme sırasında oluşturulan ADSyncAdmins.

1. Geri kopyalayarak hello veritabanını **ADSync.mdf** ve **ADSync_log.ldf** altında bulunan dosyaları `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa güvenli konumu.

2. Yeni bir PowerShell oturumu başlatın.

3. Toofolder gidin `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.

4. Başlat **sqlcmd** hello komutunu çalıştırarak yardımcı programı `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, sysadmin kimlik bilgisi hello kullanarak veya veritabanı DBO hello.

5. Merhaba sqlcmd isteminden tooshrink hello veritabanı (1 >), girin `DBCC Shrinkdatabase(ADSync,1);`, ardından `GO` hello sonraki satırda.

6. Merhaba işlemi başarılı olursa, toostart hello eşitleme hizmeti yeniden deneyin. Merhaba eşitleme hizmeti başlatmak için çok gidin[Sil'i çalıştırmak geçmiş verileri](#delete-run-history-data) adım. Değilse, desteği ile iletişime geçin.

### <a name="delete-run-history-data"></a>Geçmiş verileri çalışmasını sil
Varsayılan olarak, Azure AD Connect çalıştırma geçmişi veri tooseven günlük eşitleyeceğini korur. Bu adımda, Azure AD Connect eşitleme hizmeti yeniden eşitlemeyi başlayabilmeniz için geçmiş verileri tooreclaim DB alanı çalıştırmak hello silin.

1.  Başlat **Eşitleme Hizmeti Yöneticisi'ni** giderek tooSTART → tarafından eşitleme hizmeti.

2.  Toohello Git **Operations** sekmesi.

3.  Altında **Eylemler**seçin **Temizle çalışır**...

4.  Ya da seçebilirsiniz **tüm metinler temizleyin** veya **Temizle çalıştıran önce... <date>**  seçeneği. İki günden daha eski olan geçmiş verileri çalıştırmak temizleyerek başlatmanız önerilir. DB boyutu sorunu yaşayıp toorun devam ederseniz, hello seçin **tüm metinler temizleyin** seçeneği.

### <a name="shorten-retention-period-for-run-history-data"></a>Çalıştırma geçmişi veri saklama süresini kısaltmak
Bu adım tooreduce hello olasılığını, birden çok eşitleme döngüleri sonra hello 10 GB sınırını sorunu yaşayıp çalıştıran bağlıdır.

1. Yeni bir PowerShell oturumu açın.

2. Çalıştırma `Get-ADSyncScheduler` ve hello hello geçerli Bekletme dönemi belirtir PurgeRunHistoryInterval özelliği not edin.

3. Çalıştırma `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` tooset hello Bekletme dönemi tootwo gün. Merhaba saklama dönemi uygun şekilde ayarlayın.

## <a name="long-term-solution--migrate-toofull-sql"></a>Uzun vadeli çözüm – geçirme toofull SQL
Merhaba sorunu genel olarak, 10 GB veritabanı boyutu artık Azure AD Connect toosynchronize için yeterli olduğunu göstergesi, şirket içi Active Directory tooAzure AD. Toousing hello tam SQL server sürümü geçiş önerilir. Merhaba var olan bir Azure AD Connect dağıtıma LocalDB SQL tam sürümünü hello hello veritabanı ile doğrudan değiştirilemiyor. Bunun yerine, SQL hello tam sürümü ile yeni bir Azure AD Connect sunucusu dağıtmanız gerekir. Merhaba yeni Azure AD Connect sunucusu (SQL DB) hazırlama sunucu olarak sonraki toohello mevcut Azure AD Connect sunucusu (LocalDB) dağıtıldığı bir esnek geçiş yapmanız önerilir. 
* Uzak SQL Azure AD Connect ile nasıl tooconfigure başvurmak üzerinde yönerge için tooarticle [Azure AD Connect özel yüklemesi](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).
* Azure AD Connect yükseltmesi için esnek geçiş hakkında yönergeler için tooarticle başvuran [Azure AD Connect: son önceki bir sürüm toohello'den yükseltme](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
