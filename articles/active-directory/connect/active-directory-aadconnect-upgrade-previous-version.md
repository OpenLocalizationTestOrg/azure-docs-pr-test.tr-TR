---
title: "Azure AD Connect: Önceki bir sürümden yükseltme | Microsoft Docs"
description: "Merhaba farklı yöntemler tooupgrade toohello en son sürümü Azure Active Directory yerinde yükseltme ve esnek geçiş dahil olmak üzere Connect, açıklanmaktadır."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>Azure AD Connect: Bir önceki sürüm toohello en son yükseltme
Bu konuda, Azure Active Directory (Azure AD) Bağlan yükleme toohello en son sürüm tooupgrade kullanabileceğiniz hello farklı yöntemler açıklanmaktadır. Kendiniz hello sürümlerine sahip Azure AD Connect geçerli tutmanızı öneririz. Merhaba adımları hello de [çarpma geçiş](#swing-migration) önemli bir yapılandırma değişikliği yaptığınızda bölüm.

Dirsync'ten tooupgrade istiyorsanız, bkz: [Azure AD eşitleme aracından (DirSync) yükseltme](active-directory-aadconnect-dirsync-upgrade-get-started.md) yerine.

Azure AD Connect tooupgrade kullanabileceğiniz birkaç farklı stratejiler vardır.

| Yöntem | Açıklama |
| --- | --- |
| [Otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md) |Hızlı yükleme sahip müşteriler için hello en kolay yöntem budur. |
| [Yerinde yükseltme](#in-place-upgrade) |Tek bir sunucu varsa, üzerinde hello yükleme yerinde yükseltme yapabilirsiniz hello aynı sunucu. |
| [Esnek geçiş](#swing-migration) |İki sunucu ile Merhaba sunucularıyla hello yeni sürümü veya yapılandırma birini hazırlamak ve hazır olduğunuzda hello active server değiştirin. |

İzinleri hello bilgi için [yükseltme için gereken izinler](active-directory-aadconnect-accounts-permissions.md#upgrade).

> [!NOTE]
> Yeni Azure AD Connect sunucusu toostart eşitleme değişiklikleri tooAzure AD etkinleştirdikten sonra toousing DirSync veya Azure AD eşitleme geri gerekir. DirSync ve Azure AD eşitleme dahil olmak üzere Azure AD Connect toolegacy istemcilerden önceki sürüme indirme desteklenmiyor ve Azure AD içinde veri kaybı gibi tooissues yol açabilir.

## <a name="in-place-upgrade"></a>Yerinde yükseltme
Azure AD eşitleme veya Azure AD Connect taşımak için bir yerinde yükseltme çalışır. Forefront Identity Manager (FIM) + Azure AD Bağlayıcısı ile bir çözüm veya Dirsync'ten taşıma için çalışmıyor.

Tek bir sunucu ve değerinden yaklaşık 100.000 nesneye sahip olduğunda bu tercih edilen bir yöntemdir. Toohello out-of-box eşitleme kuralları herhangi bir değişiklik olursa, bir tam içeri aktarma ve tam eşitleme hello yükseltmeden sonra oluşur. Bu yöntem, hello yeni yapılandırmayı uygulanan tooall varolan nesneleri hello sistemde sağlar. Bu farklı çalıştır hello hello eşitleme altyapısı kapsamındaki nesnelerin sayısı bağlı olarak birkaç saat sürebilir. (Bu, varsayılan olarak 30 dakikada bir eşitlenir) hello normal delta Eşitleme Zamanlayıcısı askıya alındı, ancak parola eşitleme devam eder. Bir hafta sırasında hello yerinde yükseltme yapılması düşünebilirsiniz. Merhaba yeni Azure AD Connect sürümüyle değişiklikleri toohello out-of-box yapılandırma yoksa, sonra normal delta alma/eşitleme başlar yerine.  
![Yerinde yükseltme](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

Değişiklikleri toohello out-of-box eşitleme kuralları yaptıysanız, ardından bu kurallar geri toohello varsayılan yapılandırması yükseltme sırasında ayarlanır. toomake yapılandırmanızı yükseltmeler arasında tutulmasını açıklandığı gibi değişiklikler yapmak emin olun [en iyi uygulamalar hello varsayılan yapılandırmasını değiştirmek için](active-directory-aadconnectsync-best-practices-changing-default-configuration.md).

Yerinde yükseltme sırasında olabilir sunulan değişiklikler, yükseltme işlemi tamamlandıktan sonra çalıştırılan belirli eşitleme (tam alma adımı ve tam eşitleme adımı dahil) etkinlikleri toobe gerektirir. toodefer bu tür etkinlikler başvuran toosection [nasıl toodefer tam eşitleme yükselttikten sonra](#how-to-defer-full-synchronization-after-upgrade).

## <a name="swing-migration"></a>Swing geçişi
Karmaşık bir dağıtım veya çok sayıda nesne varsa, pratik toodo bir yerinde yükseltme hello Canlı sistem üzerinde olabilir. Bazı müşteriler için bu işlem birden fazla gün--sürebilir ve bu süre boyunca hiçbir delta değişiklikleri işlenir. Ayrıca toomake önemli değişiklikler tooyour yapılandırmasını planlama ve tootry istediğinizde bu yöntemi kullanabilirsiniz toohello bulut gönderilen önce bunları çıkışı.

yöntemi bu senaryoları için önerilen hello toouse esnek geçiş ' dir. (En az) iki sunucu--bir etkin sunucu ve bir Hazırlama sunucusu gerekir. Merhaba active server (resim aşağıdaki hello düz mavi çizgilerle gösterilir) hello etkin üretim yük sorumludur. Sunucu (kesikli mor çizgilerle gösterilir) hazırlama hello hello yeni sürüm veya yapılandırma hazırlanır. Tam olarak hazır olduğunda, bu sunucu etkinleştirilir. artık eski sürümünü veya yüklü yapılandırma hello sahiptir, hello önceki active server, hello hazırlama Server'a yapılan ve yükseltilir.

Merhaba iki sunucu farklı sürümlerini kullanabilirsiniz. Örneğin, hello active server toodecommission planlama Azure AD eşitleme kullanabilir ve Azure AD Connect hello yeni hazırlama sunucu kullanabilirsiniz. Esnek geçiş toodevelop kullanırsanız, yeni bir yapılandırma, onun bir fikir toohave üzerinde aynı sürümde hello iki sunucu hello.  
![Hazırlama sunucusu](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> Bazı müşteriler, bu senaryo için üç veya dört toohave sunucuları tercih eder. Sunucu hazırlama hello yükseltildiğinde için yedek bir sunucu yok [olağanüstü durum kurtarma](active-directory-aadconnectsync-operations.md#disaster-recovery). Üç veya dört sunucularıyla olduğundan her zaman hazır tootake üzerinden bir Hazırlama sunucusu sağlar hello yeni sürümle birincil/bekleme sunucularının bir kümesi hazırlayabilirsiniz.

Bu adımları da Azure AD eşitleme veya FIM + Azure AD Bağlayıcısı ile bir çözüm toomove çalışır. DirSync için şu adımları çalışmaz, ancak (paralel dağıtım olarak da bilinir) aynı esnek geçiş yöntemi ile DirSync için adımları hello konusu [yükseltme Azure Active Directory eşitleme (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md).

### <a name="use-a-swing-migration-tooupgrade"></a>Esnek geçiş tooupgrade kullanın
1. Azure AD Connect hem sunucu hem de planı tooonly yapma bir yapılandırma değişikliği kullanırsanız, active server ve hazırlama server hem de olduğundan emin olun kullanarak hello aynı sürümü. Daha kolay toocompare farklar daha sonra kolaylaştırır. Azure AD eşitleme'den yükseltme yapıyorsanız, bu sunucular farklı sürümlerde. Azure AD Connect eski bir sürümden yükseltirken, iyi bir fikir toostart hello iki sunucuları ile olan hello aynı sürümü kullanan, ancak gerekli değildir.
2. Özel yapılandırma yapmış olduğunuz ve hazırlama sunucunuz, yoksa, hello altındaki adımları [özel bir yapılandırma sunucusu hazırlama hello active server toohello taşıma](#move-custom-configuration-from-active-to-staging-server).
3. Azure AD Connect, önceki bir sürümünden yükseltiyorsanız, sunucu toohello en son sürümü hazırlama hello yükseltin. Azure AD eşitleme'den taşıyorsanız, Azure AD Connect'i hazırlama sunucunuza yükleyin.
4. Merhaba eşitleme Çalıştır motoru tam içeri aktarma ve tam eşitleme hazırlama sunucunuzda olanak tanır.
5. Bu hello yeni yapılandırma kaydetmedi neden beklenmeyen değişiklikleri "Doğrula" altında hello adımları kullanarak doğrulayın [sunucusunun doğrula hello yapılandırmasını](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server). Bir şeyler değilse olarak beklenen, doğru hello içeri aktarma ve eşitleme çalıştırın ve hello adımları izleyerek iyi görünüyor kadar hello verileri doğrulayın.
6. Sunucu toobe hello active server hazırlama hello geçin. Bu hello son "Anahtar active server" aşamasıdır [sunucusunun doğrula hello yapılandırmasını](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server).
7. Azure AD Connect yükseltiyorsanız, şimdi de modu toohello en son sürüm hazırlama hello sunucusunu yükseltin. Merhaba tooget hello veri ve yükseltme yapılandırma gibi önce aynı adımları izleyin. Azure AD eşitleme'den yükseltme yaptıysanız, şimdi kapatmak ve eski sunucunuz yetkisini.

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>Özel yapılandırma hello active server toohello hazırlama sunucudan taşıma
Yapılandırma değişiklikleri toohello active server yaptıysanız, toomake emin olun, aynı hello gereksinim duyduğunuz sunucu hazırlama uygulanan toohello değişir. Bu toohelp taşımak, hello kullanabileceğiniz [Azure AD Connect yapılandırma Belgeleyici'yi](https://github.com/Microsoft/AADConnectConfigDocumenter).

PowerShell kullanarak oluşturduktan hello özel eşitleme kuralları taşıyabilirsiniz. Diğer değişiklikler hello uygulamalısınız hem sistemleri ve aynı şekilde hello değişiklikleri geçirilemiyor. Merhaba [yapılandırma Belgeleyici'yi](https://github.com/Microsoft/AADConnectConfigDocumenter) hello iki sistemleri toomake aynı olduklarından emin karşılaştırma yardımcı olabilir. Bu bölümde bulunan hello adımlarını otomatik hale getirmede Hello aracı de yardımcı olabilir.

Tooconfigure hello aşağıdakiler şeyler hello aynı şekilde her iki sunucuda:

* Bağlantı toohello aynı ormanlar
* Tüm etki alanı ve OU filtreleme
* Parola Eşitleme ve parola geri yazma gibi aynı isteğe bağlı özellikler hello

**Özel eşitleme kuralları taşıma**  
toomove özel eşitleme kuralları hello aşağıdaki:

1. Açık **eşitleme kuralları Düzenleyicisi** etkin sunucunuzda.
2. Özel bir kural seçin. Tıklatın **verme**. Bir not defteri pencereyi getirir. Merhaba geçici dosya bir PS1 uzantısıyla kaydedin. Bu, bir PowerShell komut dosyası sağlar. Sunucu hazırlama hello PS1 dosyası toohello kopyalayın.  
   ![Eşitleme kuralı dışarı aktarma](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. Merhaba bağlayıcı GUID sunucu hazırlama hello üzerinde farklıdır ve değiştirmeniz gerekir. tooget hello GUID, başlangıç **eşitleme kuralları Düzenleyicisi**, hello out-of-box kurallardan biri aynı bağlı sistem ve'ı tıklatın, temsil hello seçin **verme**. Merhaba PS1 dosyanızdaki GUID hello GUID hello sunucu hazırlama alanından değiştirin.
4. Bir PowerShell komut isteminde hello PS1 dosyasını çalıştırın. Bu, sunucu hazırlama hello üzerinde hello özel eşitleme kuralı oluşturur.
5. Bu, özel kurallarınızı için işlemi yineleyin.

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>Nasıl toodefer tam eşitleme yükselttikten sonra
Yerinde yükseltme sırasında olabilir yürütülen belirli eşitleme (tam alma adımı ve tam eşitleme adımı dahil) etkinlikleri toobe gerektiren sunulan değişiklikler. Örneğin, bağlayıcı şema değişiklikleri gerektirir **tam alma** adım ve out-of-box eşitleme kuralı değişiklik gerektiren **tam eşitleme** etkilenen bağlayıcıların yürütülen toobe adım. Yükseltme sırasında Azure AD Connect eşitleme etkinlikleri gerekli olduğunu belirler ve bunları olarak kaydeder *geçersiz kılmaları*. Merhaba, eşitleme döngüsü aşağıdaki hello Eşitleme Zamanlayıcısı bu geçersiz kılma işlemleri seçer ve bunları yürütür. Bir geçersiz kılma başarılı bir şekilde yürütüldükten sonra kaldırılır.

Burada, bu geçersiz kılmaları tootake yer hemen yükseltmeden sonra istemediğiniz durumlar olabilir. Örneğin, çok sayıda eşitlenmiş nesneleri varsa ve bu eşitleme adımları toooccur çalışma saatlerinden istersiniz. Bu geçersiz kılmaları tooremove:

1. Yükseltme sırasında **işaretini** hello seçeneği **Yapılandırma tamamlandığında hello eşitleme işlemini başlatmak**. Bu hello Eşitleme Zamanlayıcısı'nı devre dışı bırakır ve hello geçersiz kılmaları kaldırılmadan önce eşitleme döngüsü alma yerden otomatik olarak engeller.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. Yükseltme tamamlandıktan sonra hangi geçersiz kılmaları eklenen çıkışı cmdlet toofind aşağıdaki hello çalıştırın:`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > Merhaba geçersiz kılmaları bağlayıcı özgüdür. Hello aşağıdaki örnekte, tam alma adımı ve tam eşitleme adım tooboth hello şirket içi AD Bağlayıcısı eklenmiştir ve Azure AD Bağlayıcısı.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. Eklenen hello varolan geçersiz kılmaları unutmayın.
   
4. tam içeri aktarma ve hello aşağıdaki cmdlet'i çalıştırın, rasgele bir bağlayıcı üzerinde tam eşitleme tooremove hello kılmalarının:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   tüm bağlayıcılar üzerinde tooremove hello geçersiz kılmaları PowerShell Betiği aşağıdaki hello yürütün:

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. tooresume hello Zamanlayıcı ' hello aşağıdaki cmdlet'i çalıştırın:`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > Erken kolaylık tooexecute gerekli hello eşitleme adımları unutmayın. El ile hello Eşitleme Hizmeti Yöneticisi'ni kullanarak aşağıdaki adımları yürütme veya geri hello kümesi ADSyncSchedulerConnectorOverride cmdlet'ini kullanarak hello geçersiz kılmaları ekleyin.

tam içeri aktarma ve hello aşağıdaki cmdlet'i çalıştırın, rasgele bir bağlayıcı üzerinde tam eşitleme tooadd hello kılmalarının:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).
