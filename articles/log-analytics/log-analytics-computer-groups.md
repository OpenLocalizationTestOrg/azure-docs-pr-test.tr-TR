---
title: "Günlük analizi aaaComputer gruplarında oturum aramaları | Microsoft Docs"
description: "Günlük analizi bilgisayar gruplarında tooscope günlük aramaları tooa belirli bir bilgisayarlar kümesi sağlar.  Bu makalede hello farklı yöntemler toocreate bilgisayar grupları ve toouse nasıl günlüğü arama kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Günlük analizi bilgisayar gruplarında aramaları oturum

>[!NOTE]
> Bu makalede, bilgisayar gruplarını hello geçerli günlük Anayltics sorgu dili kullanarak hello kullanımını açıklar.    Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sonra da bilgisayar grupları farklı şekillerde çalışır.  Notlar hello yeni sorgu dili için bu makalede hello farklı sözdizimi ve davranış ile sağlanır.  


Günlük analizi bilgisayar gruplarında tooscope izin [oturum aramaları](log-analytics-log-searches.md) tooa belirli bilgisayarlar kümesi.  Her Grup ya da tanımladığınız bir sorgu kullanarak bilgisayarları veya grupları farklı kaynaklardan alarak doldurulur.  Merhaba Grup günlük aramada dahil edildiğinde hello sonuçlar hello grubundaki hello bilgisayarlar eşleşen sınırlı toorecords olur.

## <a name="creating-a-computer-group"></a>Bir bilgisayar grubu oluşturma
Günlük analizi aşağıdaki tablonun hello hello yöntemlerden birini kullanarak bir bilgisayar grubu oluşturabilirsiniz.  Aşağıdaki hello bölümler her yöntem hakkında ayrıntılar sağlanmaktadır. 

| Yöntem | Açıklama |
|:--- |:--- |
| Günlük araması |Bilgisayar listesi döndüren bir günlük arama oluşturun ve hello sonuçları bir bilgisayar grubu olarak kaydedin. |
| Log Arama API’si |Kullanım hello günlük arama API tooprogrammatically hello günlük arama sonuçlarına dayalı bir bilgisayar grubu oluşturun. |
| Active Directory |Otomatik olarak bir Active Directory etki alanının üyesi olan ve bir grubu günlük analizi için her güvenlik grubu oluşturun. Aracı bilgisayarların hello grup üyeliğini tarayın. |
| WSUS |Otomatik olarak grupları hedeflemek için WSUS sunucularını veya istemcilerini taramak ve günlük analizi her biri için bir grup oluşturun. |

### <a name="log-search"></a>Günlük araması
Bilgisayar grupları günlük aramadan oluşturulan tüm tanımladığınız bir arama sorgusu tarafından döndürülen hello bilgisayarları içerir.  Bu sorgu hello bilgisayar grubu Hello Grup oluşturulduktan sonra herhangi bir değişiklik yansıtılır böylece her kullanılışında çalıştırılır.

Bir günlük aramadan yordamı toocreate bir bilgisayar grubu aşağıdaki hello kullanın.

1. [Günlük bir arama oluştururken](log-analytics-log-searches.md) bilgisayarların bir listesini döndürür.  Merhaba arama bilgisayarlar ayrı bir dizi benzeri kullanarak döndürmelidir **farklı bilgisayar** veya **bilgisayar tarafından count() ölçmek** hello sorgu.  
2. Merhaba tıklatın **kaydetmek** Merhaba ekranında hello üstündeki düğmesi.
3. Seçin **Evet** çok**bu sorguyu bir bilgisayar grubu olarak kaydetmek**.
4. Yazın bir **adı** ve **kategori** hello grubu için.  Aynı ada ve kategoriye bir arama zaten hello olan olması ardından istendiğinde toooverwrite, varsa.  Merhaba farklı kategorilerde aynı ad ile birden çok araması olabilir. 

Bir bilgisayar grubu olarak kaydedebilirsiniz örnek aramalar aşağıda verilmiştir.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md) hello aşağıdaki değişiklikleri yapılmış toohello yordamı toocreate yeni bir bilgisayar grubu sonra.
>  
> - bir bilgisayar grubu içermelidir sorgu toocreate hello `distinct Computer`.  Aşağıdaki sorgu toocreate bir bilgisayar grubu örneğidir.<br>`Heartbeat | where Computer contains "srv" `
> - Yeni bir bilgisayar grubu oluşturduğunuzda, bir diğer ad toplama toohello adı belirtmeniz gerekir.  Aşağıda açıklandığı gibi hello bilgisayar grubu sorguda kullanırken, hello diğer adı kullanın.  

### <a name="log-search-api"></a>Günlük arama API
Günlük arama API olan hello ile oluşturulmuş bilgisayar gruplarına aynı günlük arama ile oluşturulan arama olarak hello.

Merhaba günlük arama API kullanarak bir bilgisayar grubu oluşturma hakkında bilgi için bkz [bilgisayar grupları günlük analizi günlüğünde arama REST API](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Active Directory
Günlük analizi tooimport Active Directory grup üyeliklerini yapılandırırken, etki alanına katılmış bilgisayarlara hello OMS Aracısı ile Merhaba grup üyeliğini analiz eder.  Bir bilgisayar grubu Active Directory'de her güvenlik grubu için günlük analizi oluşturulur ve her bilgisayar toohello güvenlik gruplarının üyesi olan karşılık gelen toohello bilgisayar gruplarına eklenir.  Bu üyelik sürekli olarak 4 saatte bir güncelleştirilir.  

Günlük analizi tooimport Active Directory güvenlik gruplarını hello gelen yapılandırma **bilgisayar grupları** günlük analizi menüde **ayarları**.  Seçin **Otomasyon** ve ardından **alma Active Directory grup üyeliklerini bilgisayarlardan**.  Başka bir yapılandırma işlemi gerekmez.

![Bilgisayar grupları Active Directory'den](media/log-analytics-computer-groups/configure-activedirectory.png)

Grupları alındıktan, hello menü listeleri hello grup üyeliği ile bilgisayar sayısını algılanır ve içe grup sayısı hello.  Bu bağlantılar tooreturn hello birini tıklatın **ComputerGroup** bu bilgilerle kaydeder.

### <a name="windows-server-update-service"></a>Windows Server Update Service
Yapılandırırsanız, günlük analizi tooimport WSUS grup üyeliklerini, hello OMS Aracısı sahip tüm bilgisayarların grup üyeliği hedefleme hello analiz eder.  İstemci-tarafı kullanıyorsanız hedefleme, bağlı tooOMS ve grupları hedefleme WSUS parçası olan herhangi bir bilgisayar grup üyeliğini tooLog Analytics aldı. Sunucu tarafı kullanıyorsanız hedefleme, WSUS hello üzerinde OMS Aracısı yüklenmesi gereken hello sunucu hello grup üyeliği bilgileri toobe sırada tooOMS alındı.  Bu üyelik sürekli olarak 4 saatte bir güncelleştirilir. 

Günlük analizi tooimport Active Directory güvenlik gruplarını hello gelen yapılandırma **bilgisayar grupları** günlük analizi menüde **ayarları**.  Seçin **Active Directory** ve ardından **alma Active Directory grup üyeliklerini bilgisayarlardan**.  Başka bir yapılandırma işlemi gerekmez.

![Bilgisayar grupları Active Directory'den](media/log-analytics-computer-groups/configure-wsus.png)

Grupları alındıktan, hello menü listeleri hello grup üyeliği ile bilgisayar sayısını algılanır ve içe grup sayısı hello.  Bu bağlantılar tooreturn hello birini tıklatın **ComputerGroup** bu bilgilerle kaydeder.

## <a name="managing-computer-groups"></a>Bilgisayar gruplarını yönetme
Bir günlük aramadan oluşturulan bilgisayar gruplarını görüntülemek veya günlük arama API hello hello **bilgisayar grupları** günlük analizi menüde **ayarları**.  Merhaba tıklatın **x** hello içinde **kaldırmak** sütun toodelete hello bilgisayar grubu.  Hello tıklatın **görüntülemek üyeleri** üyeleri döndürür Grup toorun hello grubun günlük arama simgesi. 

![Kayıtlı bilgisayar gruplarını](media/log-analytics-computer-groups/configure-saved.png)

toomodify hello grubunda, yeni bir hello ile aynı grup **kategori** ve **adı** toooverwrite hello özgün grup.

## <a name="using-a-computer-group-in-a-log-search"></a>Bir bilgisayar grubu günlük aramada kullanma
Sözdizimi toorefer tooa bilgisayar günlük arama grubunda aşağıdaki hello kullanın.  Belirten hello **kategori** isteğe bağlıdır ve yalnızca bilgisayar grupları ile aynı adı farklı kategorilerde hello varsa gerekli değil. 

    $ComputerGroups[Category: Name]

Bir aramayı çalıştırırken, hello hello aramasına dahil tüm bilgisayar gruplarının üyeleri ilk çözümlenir.  Ardından Hello Grup bir günlük arama temel alıyorsa, bu arama hello en üst düzey günlük arama yapmadan önce tooreturn hello hello grubunun üyeleri çalıştırılır.

Bilgisayar grupları genelde hello ile kullanılan **IN** aşağıdaki örneğine hello olduğu gibi hello günlük arama yan tümcesinde:

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), aşağıdaki örneğine hello gibi bir işlevi olarak diğer adını düşünerek sorguda bir bilgisayar grubunu kullanmak sonra:
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>Bilgisayar grubu kaydı
Bir kayıt için Active Directory veya WSUS oluşturulan her bilgisayar grubu üyeliği hello OMS depo oluşturulur.  Bu kayıtları bir türüne sahip **ComputerGroup** ve aşağıdaki tablonun hello hello özelliklere sahiptir.  Kayıtları günlük aramaları tabanlı bilgisayar gruplarının oluşturulmaz.

| Özellik | Açıklama |
|:--- |:--- |
| Tür |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| Bilgisayar |Merhaba üye bilgisayarın adı. |
| Grup |Merhaba grubunun adı. |
| GroupFullName |Tam yol toohello grubu Hello kaynak ve kaynak adı dahil olmak üzere. |
| GroupSource |Bu grup kaynak gelen toplanan oluştu. <br><br>Active Directory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |Grup hello hello kaynağının adını toplandığı.  Active Directory'de, bu hello etki alanı adıdır. |
| ManagementGroupName |SCOM aracılar için hello yönetim grubunun adı.  Diğer aracılar için AOI - budur\<çalışma alanı kimliği\> |
| TimeGenerated |Tarih ve saat hello bilgisayar grubu oluşturulurken veya güncelleştirilirken. |

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.  

