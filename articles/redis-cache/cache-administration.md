---
title: "Azure Redis önbelleği aaaHow tooadminister | Microsoft Docs"
description: "Azure Redis önbelleği için zamanlama güncelleştirir ve nasıl tooperform yönetim görevlerini gibi yeniden bilgi edinin"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>Nasıl tooadminister Azure Redis önbelleği
Bu konu, nasıl tooperform yönetim gibi görevleri açıklar [yeniden](#reboot) ve [güncelleştirmeleri zamanlama](#schedule-updates) Azure Redis önbelleği örnekleri için.

## <a name="reboot"></a>Yeniden başlatma
Merhaba **yeniden** dikey tooreboot sağlar, önbelleğin bir veya daha fazla düğüm. Bir önbellek düğümü ise bu yeniden başlatma yeteneği, tootest, uygulamanız için esneklik sağlar.

![Yeniden başlatma](./media/cache-administration/redis-cache-administration-reboot.png)

Hello düğümleri tooreboot tıklatıp **yeniden**.

![Yeniden başlatma](./media/cache-administration/redis-cache-reboot.png)

Kümeleme özelliği etkinleştirilmiş bir premium önbelleği varsa, hangi parça hello önbellek tooreboot birini seçebilirsiniz.

![Yeniden başlatma](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot, önbellek, bir veya daha fazla düğümlerinin istenen hello düğümleri tıklatıp **yeniden**. Kümeleme özelliği etkinleştirilmiş bir premium önbelleği varsa desired hello parça tooreboot seçin ve ardından **yeniden**. Birkaç dakika sonra seçili düğümler yeniden başlatma hello ve birkaç dakika sonra yeniden çevrimiçi.

istemci uygulamaları Hello etkisini, yeniden hangi düğümlerin bağlı olarak değişir.

* **Ana** - hello ana düğüm toohello çoğaltma düğüm üzerinde yeniden başlatılan, Azure Redis önbelleği başarısız olduğunda ve toomaster yükseltir. Bu yük devretme sırasında toohello önbellek bağlantı başarısız olabileceği kısa bir aralık olabilir.
* **Bağımlı** - hello ikincil düğüm yeniden başlatıldığında, hiçbir etkisi toocache istemci yoktur.
* **Hem ana hem de ikincil** - iki önbellek düğümleri yeniden başlatılır, tüm verileri hello birincil düğüm tekrar çevrimiçi gelene kadar hello önbellek ve bağlantıları toohello önbellek başarısız kaybolur. Yapılandırdıysanız [veri kalıcılığını](cache-how-to-premium-persistence.md), hello en son yedeklemenin geri hello önbellek tekrar çevrimiçi gelir, ancak hello en son yedeklemeden sonra gerçekleşen tüm önbellek yazma kaybolur.
* **Premium düğümlerinin önbelleğe kümeleme özelliği etkinleştirilmiş** - bir yeniden başlatma veya daha fazla düğüm Kümeleme ile bir premium önbelleği etkinse, seçili hello davranışını hello düğümleri olduğu hello aynı olduğunda, hello karşılık gelen veya kümelenmemiş, düğümü yeniden başlatma önbelleği.

> [!IMPORTANT]
> Yeniden başlatma için tüm fiyatlandırma katmanlarına kullanıma sunulmuştur.
> 
> 

## <a name="reboot-faq"></a>Yeniden başlatma ile ilgili SSS
* [Hangi düğümün ı tootest Uygulamam yeniden başlatma?](#which-node-should-i-reboot-to-test-my-application)
* [Merhaba önbellek tooclear istemci bağlantılarını yeniden başlatılabilir?](#can-i-reboot-the-cache-to-clear-client-connections)
* [Yeniden başlatma işlemi yaparsanız ı my önbellekten veri kaybedeceksiniz?](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [PowerShell'i, CLI veya diğer yönetim araçlarını kullanarak my önbelleği yeniden başlatılabilir?](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [Hangi fiyatlandırma katmanlarını hello yeniden başlatma işlevselliği kullanabilir miyim?](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>Hangi düğümün ı tootest Uygulamam yeniden başlatma?
Uygulamanızın arızasına karşı hello birincil düğümü yeniden başlatma hello önbelleğinizin tootest hello dayanıklılık **ana** düğümü. Uygulamanızın arızasına karşı hello ikincil düğümü, yeniden başlatma hello tootest hello dayanıklılık **bağımlı** düğümü. tootest hello dayanıklılık uygulamanızın hello önbelleğinin toplam arızasına karşı yeniden başlatma **her ikisi de** düğümleri.

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>Merhaba önbellek tooclear istemci bağlantılarını yeniden başlatılabilir?
Evet, tüm istemci bağlantıları hello önbellek yeniden başlatırsanız temizlenir. Yeniden başlatma tüm istemci bağlantıları tooa mantık hatası ya da hello istemci uygulamasında hata nedeniyle kullanıldığı hello durumda yararlı olabilir. Her fiyatlandırma katmanının farklı olan [istemci bağlantı sınırlarını](cache-configure.md#default-redis-server-configuration) hello çeşitli boyutlarda ve bu sınırları ulaşıldığında, daha fazla hiçbir istemci bağlantılarını kabul edilir. Merhaba önbellek yeniden yolu tooclear tüm istemci bağlantıları sağlar.

> [!IMPORTANT]
> Önbellek tooclear istemci bağlantılarınızı yeniden başlatırsanız hello Redis düğüm tekrar çevrimiçi olduğunda StackExchange.Redis otomatik olarak yeniden bağlanır. Merhaba temel sorun giderilmezse hello istemci bağlantıları kullanılan toobe devam edebilir.
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>Yeniden başlatma işlemi yaparsanız ı my önbellekten veri kaybedeceksiniz?
Her iki hello yeniden başlatırsanız **ana** ve **bağımlı** düğümleri hello önbelleği (veya premium önbelleği kümeleme özelliği etkinleştirilmiş kullanıyorsanız bu parça) tüm veriler kaybolur. Yapılandırdıysanız [veri kalıcılığını](cache-how-to-premium-persistence.md), hello önbellek tekrar çevrimiçi gelir, ancak hello yedekleme yapıldıktan sonra oluşan önbellek yazma kaybolur hello en son yedeklemenin geri yüklenir.

Hello düğümleri yalnızca birini yeniden başlatırsanız, veri genellikle kaybı olmaz ancak hala olabilir. Örneğin Hello ana düğüm yeniden ve önbellek yazma, hello önbellek yazma hello verilerden ediyor kaybolduğu için. Veri kaybı için başka bir senaryo, bir düğümü yeniden başlatma ve diğer hello düğümü olur toogo aşağı tooa hatası hello en son olacaktır aynı anda. Veri kaybı olası nedenleri hakkında daha fazla bilgi için bkz: [Redis ne oldu toomy verileri?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>PowerShell'i, CLI veya diğer yönetim araçlarını kullanarak my önbelleği yeniden başlatılabilir?
Evet, yönergeler için PowerShell bkz [tooreboot Redis önbelleği](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>Hangi fiyatlandırma katmanlarını hello yeniden başlatma işlevselliği kullanabilir miyim?
Yeniden başlatma tüm fiyatlandırma katmanları için kullanılabilir.

## <a name="schedule-updates"></a>Güncelleştirmeleri zamanlama
Merhaba **zamanlama güncelleştirmeleri** dikey toodesignate Premium katmanı önbelleğiniz için bir bakım penceresi sağlar. Merhaba bakım penceresi belirtildiğinde, herhangi bir Redis sunucu güncelleştirme sırasında bu pencereyi yapılır. 

> [!NOTE] 
> Merhaba bakım penceresi yalnızca tooRedis server güncelleştirmeleri ve değil Azure güncelleştirir veya hello önbelleği barındırmak hello VM'lerin toohello işletim sistemi güncelleştirmelerini tooany geçerlidir.
> 
> 

![Güncelleştirmeleri zamanlama](./media/cache-administration/redis-schedule-updates.png)

toospecify bir bakım penceresi istenen hello gün kontrol edin ve her gün için hello bakım penceresi başlangıç saati belirtin ve tıklatın **Tamam**. Merhaba bakım penceresi saati UTC biçiminde olduğunu unutmayın. 

> [!NOTE]
> Merhaba varsayılan bakım penceresi güncelleştirmeleri için beş saattir. Bu değer hello Azure portal ' yapılandırılabilir değildir, ancak hello kullanarak PowerShell'de yapılandırabilirsiniz `MaintenanceWindow` hello parametresinin [yeni AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet'i. Daha fazla bilgi için bkz: [PowerShell'i, CLI veya diğer yönetim araçlarını kullanarak zamanlanmış güncelleştirmeler yönetebilirim?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)
> 
> 

## <a name="schedule-updates-faq"></a>Güncelleştirmeleri zamanla SSS
* [Merhaba zamanlama güncelleştirme özelliğini kullanmıyorsanız güncelleştirmeler olduğunda?](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [Güncelleştirmeleri ne tür hello sırasında yapılan bakım penceresi zamanlanmış?](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [Zamanlanmış güncelleştirmeler PowerShell'i, CLI veya diğer yönetim araçlarını kullanarak yönetebilir miyim?](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [Hangi fiyatlandırma katmanlarını hello zamanlama Güncelleştirmeler işlevini kullanabilir miyim?](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>Merhaba zamanlama güncelleştirme özelliğini kullanmıyorsanız güncelleştirmeler olduğunda?
Bir bakım penceresi belirtmezseniz, güncelleştirmelerinin herhangi bir zamanda yapılabilir.

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>Güncelleştirmeleri ne tür hello sırasında yapılan bakım penceresi zamanlanmış?
Yalnızca sunucu güncelleştirmeleri hello zamanlanmış bakım penceresi sırasında yapılan Redis. Merhaba bakım penceresi tooAzure güncelleştirmeleri uygulanmaz veya toohello VM işletim sistemi güncelleştirir.

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>Zamanlanmış güncelleştirmeler PowerShell'i, CLI veya diğer yönetim araçlarını kullanarak yönetilen alabilirim?
Evet, PowerShell cmdlet'leri aşağıdaki hello kullanarak, Zamanlanmış güncelleştirmeleri yönetebilirsiniz:

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [AzureRmRedisCachePatchSchedule yeni](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [AzureRmRedisCacheScheduleEntry yeni](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Remove-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>Hangi fiyatlandırma katmanlarını hello zamanlama Güncelleştirmeler işlevini kullanabilir miyim?
Merhaba **zamanlama güncelleştirmeleri** özelliktir yalnızca hello premium fiyatlandırma katmanına kullanılabilir.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla araştırmak [Azure Redis önbelleği premium katmanına](cache-premium-tier-intro.md) özellikleri.

