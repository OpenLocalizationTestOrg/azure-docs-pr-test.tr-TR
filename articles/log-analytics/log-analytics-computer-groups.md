---
title: "Azure günlük analizi bilgisayar gruplarında oturum aramaları | Microsoft Docs"
description: "Günlük analizi bilgisayar gruplarında, belirli bir bilgisayar kümesi kapsam günlük aramaları izin verir.  Bu makalede, bilgisayar grupları ve günlük aramada kullanma oluşturmak için kullanabileceğiniz farklı yöntemler açıklanmaktadır."
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
ms.date: 01/09/2018
ms.author: bwren
ms.openlocfilehash: 4d6a80082711f09e9c189d53fb4fda00a7d73c29
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/10/2018
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Günlük analizi bilgisayar gruplarında aramaları oturum

Günlük analizi bilgisayar gruplarında kapsamına izin [oturum aramaları](log-analytics-log-search-new.md) bilgisayarları belirli bir dizi.  Her Grup ya da tanımladığınız bir sorgu kullanarak bilgisayarları veya grupları farklı kaynaklardan alarak doldurulur.  Grubun bir günlük aramasına dahil olduğu zaman sonuçları gruptaki bilgisayarların eşleşen kayıtları sınırlıdır.

## <a name="creating-a-computer-group"></a>Bir bilgisayar grubu oluşturma
Günlük analizi yöntemlerden birini kullanarak aşağıdaki tabloda, bir bilgisayar grubu oluşturabilirsiniz.  Her yöntem hakkında ayrıntılar aşağıdaki bölümlerde verilmiştir. 

| Yöntem | Açıklama |
|:--- |:--- |
| Günlük araması |Bilgisayar listesi döndüren bir günlük arama oluşturun. |
| Log Arama API’si |Program aracılığıyla bir günlük arama sonuçlarına dayalı bir bilgisayar grubu oluşturmak için günlük arama API kullanın. |
| Active Directory |Otomatik olarak bir Active Directory etki alanının üyesi olan ve bir grubu günlük analizi için her güvenlik grubu oluşturun. Aracı bilgisayarların grup üyeliği tarayın. |
| Configuration Manager | System Center Configuration Manager koleksiyonları içeri aktarmak ve günlük analizi her biri için bir grup oluşturun. |
| Windows Server Update Services |Otomatik olarak grupları hedeflemek için WSUS sunucularını veya istemcilerini taramak ve günlük analizi her biri için bir grup oluşturun. |

### <a name="log-search"></a>Günlük araması
Bir günlük aramadan oluşturulmuş bilgisayar gruplarına tanımladığınız bir sorgu tarafından döndürülen tüm bilgisayarların içerir.  Bu sorgu bilgisayar grubunu Grup oluşturulduktan sonra herhangi bir değişiklik yansıtılır böylece her kullanılışında çalıştırılır.  

Bir bilgisayar grubu için herhangi bir sorgu kullanabilirsiniz, ancak ayrı bir bilgisayar kümesi kullanarak döndürmelidir `distinct Computer`.  Bir bilgisayar grubu olarak için kullanabilir bir örnek arama aşağıdadır.

    Heartbeat | where Computer contains "srv" | distinct Computer

Aşağıdaki tabloda, bir bilgisayar grubu tanımlayan özellikleri açıklanmaktadır.

| Özellik | Açıklama |
|:---|:---|
| Görünen Ad   | Portalda görüntülemek için arama adı. |
| Kategori       | Portal aramalarda düzenlemek için kategori. |
| Sorgu          | Bilgisayar grubu için sorgu. |
| İşlev diğer adı | Sorguda bilgisayar grubu tanımlamak için kullanılan benzersiz bir diğer ad. |

Azure portalında bir günlük aramadan bir bilgisayar grubu oluşturmak için aşağıdaki yordamı kullanın.

2. Açık **günlük arama** ve ardından **kayıtlı aramaları** ekranın üstünde.
3. Tıklatın **Ekle** ve bilgisayar grubu için her bir özellik için değerler sağlayın.
4. Seçin **bu sorguyu bir bilgisayar grubu olarak kaydetmek** tıklatıp **Tamam**.


Günlük arama OMS portalında bir bilgisayar grubu oluşturmak için aşağıdaki yordamı kullanın.

1. Açık **günlük arama** ve bilgisayar grubu için günlük arama oluşturun.  
2. Tıklatın **kaydetmek** ekranın üstündeki düğmesi.
3. Seçin **Evet** için **bu sorguyu bir bilgisayar grubu olarak kaydetmek**.
5. Bilgisayar grubu için her bir özellik için değerleri girin. 


>[!NOTE]
> Çalışma alanınızı hala kullanıyorsa [eski günlük analizi sorgu dili](log-analytics-log-search-upgrade.md) bir bilgisayar grubu oluşturmak için aynı yordamı kullanın ancak, eski sorgu dili sözdizimi kullanmanız gerekir.


### <a name="log-search-api"></a>Günlük arama API
Bilgisayar grupları günlük arama API ile oluşturulan bir günlük arama ile oluşturulan arama ile aynıdır.  Günlük arama API kullanarak bir bilgisayar grubu oluşturma ile ilgili ayrıntılar için bkz [bilgisayar grupları günlük analizi günlüğünde arama REST API](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Active Directory
Active Directory grup üyeliklerini içeri aktarmak için günlük analizi yapılandırırken, etki alanına katılmış bilgisayarlara OMS Aracısı ile grup üyeliğini analiz eder.  Bir bilgisayar grubu Active Directory'de her güvenlik grubu için günlük analizi oluşturulur ve her bilgisayar bilgisayar gruplarına üye olan güvenlik gruplarına karşılık gelen eklenir.  Bu üyelik sürekli olarak 4 saatte bir güncelleştirilir.  

Active Directory güvenlik grupları günlük analizi almak için günlük analizi yapılandırma **Gelişmiş ayarları** Azure portalında.  Seçin **bilgisayar grupları**, **Active Directory**ve ardından **alma Active Directory grup üyeliklerini bilgisayarlardan**.  Başka bir yapılandırma işlemi gerekmez.

![Bilgisayar grupları Active Directory'den](media/log-analytics-computer-groups/configure-activedirectory.png)

Gruplar içe aktarılırken menüsü algılanan grup üyeliğine sahip bilgisayarların sayısını ve içe grupları listeler.  Ya geri dönmek için bu bağlantıları tıklatabilirsiniz **ComputerGroup** bu bilgilerle kaydeder.

### <a name="windows-server-update-service"></a>Windows Server Update Service
WSUS grup üyeliklerini içeri aktarmak için günlük analizi yapılandırdığınızda, bilgisayarlara OMS Aracısı ile hedefleme grup üyeliğini analiz eder.  İstemci-tarafı kullanıyorsanız hedefleme, günlük Analizi'ne bağlı ve tüm WSUS parçası olan herhangi bir bilgisayar gruplarını hedefleme için günlük analizi içe grup üyeliğine sahiptir. Sunucu tarafı kullanıyorsanız hedefleme, OMS Aracısı sırada grup üyeliği bilgileri için günlük analizi aktarılması için WSUS sunucusunda yüklenmelidir.  Bu üyelik sürekli olarak 4 saatte bir güncelleştirilir. 

Günlük analizi ' içe aktarma WSUS grupları için günlük analizi yapılandırma **Gelişmiş ayarları** Azure portalında.  Seçin **bilgisayar grupları**, **WSUS**ve ardından **içeri aktarma WSUS grup üyeliklerini**.  Başka bir yapılandırma işlemi gerekmez.

![WSUS bilgisayar gruplarından](media/log-analytics-computer-groups/configure-wsus.png)

Gruplar içe aktarılırken menüsü algılanan grup üyeliğine sahip bilgisayarların sayısını ve içe grupları listeler.  Ya geri dönmek için bu bağlantıları tıklatabilirsiniz **ComputerGroup** bu bilgilerle kaydeder.

### <a name="system-center-configuration-manager"></a>System Center Configuration Manager
Configuration Manager koleksiyon üyelikleri almak için günlük analizi yapılandırdığınızda, her koleksiyon için bir bilgisayar grubu oluşturur.  Koleksiyon üyeliği bilgilerini, bilgisayar gruplarını güncel kalmasını sağlamak için 3 saatte alınır. 

Configuration Manager koleksiyonları içeri aktarmadan önce şunları yapmalısınız [Configuration Manager günlük Analizi'ne bağlamak](log-analytics-sccm.md).  Daha sonra günlük analizi alma yapılandırabilirsiniz **Gelişmiş ayarları** Azure portalında.  Seçin **bilgisayar grupları**, **SCCM**ve ardından **alma Configuration Manager koleksiyon üyelikleri**.  Başka bir yapılandırma işlemi gerekmez.

![SCCM bilgisayar gruplarından](media/log-analytics-computer-groups/configure-sccm.png)

Koleksiyonları içeri aktardığınızda menüsü algılanan grup üyeliğine sahip bilgisayarların sayısını ve içe grupları listeler.  Ya geri dönmek için bu bağlantıları tıklatabilirsiniz **ComputerGroup** bu bilgilerle kaydeder.

## <a name="managing-computer-groups"></a>Bilgisayar gruplarını yönetme
Günlük arama veya günlük analizi günlük arama API'SİNDEN oluşturulan bilgisayar grupları görüntüleyebilirsiniz **Gelişmiş ayarları** Azure portalında.  Seçin **bilgisayar grupları** ve ardından **grupları kaydedilmiş**.  

Tıklatın **x** içinde **kaldırmak** bilgisayar grubunu silmek için sütun.  Tıklatın **görüntülemek üyeleri** üyeleri döndürür grubun günlük arama çalıştırmak bir grubu simgesi.  Bir bilgisayar grubu değiştirilemez, ancak bunun yerine gerekir silin ve değiştirilen ayarlarla yeniden oluşturun.

![Kayıtlı bilgisayar gruplarını](media/log-analytics-computer-groups/configure-saved.png)


## <a name="using-a-computer-group-in-a-log-search"></a>Bir bilgisayar grubu günlük aramada kullanma
Genellikle aşağıdaki sözdizimi ile birlikte bir işlevi olarak diğer adını düşünerek günlük arama sorguda oluşturulan bir bilgisayar grubu kullanın:

  `Table | where Computer in (ComputerGroup)`

Örneğin, yalnızca bilgisayarlar için UpdateSummary kayıtları mycomputergroup adlı bir bilgisayar grubunda döndürmek için aşağıdaki kullanabilirsiniz.
 
  `UpdateSummary | where Computer in (mycomputergroup)`


İçeri aktarılan bilgisayar grupları ve dahil edilen bilgisayarlarında depolanır **ComputerGroup** tablo.  Örneğin, aşağıdaki sorguyu bilgisayarların bir listesini Active Directory'den etki alanı bilgisayarları grubunda döndürecektir. 

  `ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "Domain Computers" | distinct Computer`

Aşağıdaki sorgu UpdateSummary kayıtları yalnızca bilgisayarlar için etki alanı bilgisayarları döndürür.

  ```
  let ADComputers = ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "Domain Computers" | distinct Computer;
  UpdateSummary | where Computer in (ADComputers)
  ```



  

>[!NOTE]
> Çalışma alanınızı hala kullanıyorsa [eski günlük analizi sorgu dili](log-analytics-log-search-upgrade.md)>, sonra da günlük aramada bilgisayar grubuna başvurmak için aşağıdaki sözdizimini kullanın.  Belirtme **kategori** > isteğe bağlıdır ve yalnızca bilgisayar grupları aynı ada sahip farklı kategorilerde varsa gerekli değil. 
>
>    `$ComputerGroups[Category: Name]`
>
>Bilgisayar grupları ile kullanılan genellikle **IN** aşağıdaki örnekteki gibi günlük arama yan tümcesinde:
>
>    `Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]`



## <a name="computer-group-records"></a>Bilgisayar grubu kaydı
Active Directory veya WSUS oluşturulan her bilgisayar grubu üyeliği için günlük analizi çalışma alanındaki bir kayıt oluşturulur.  Bu kayıtları bir türüne sahip **ComputerGroup** ve aşağıdaki tabloda özelliklere sahiptir.  Kayıtları günlük aramaları tabanlı bilgisayar gruplarının oluşturulmaz.

| Özellik | Açıklama |
|:--- |:--- |
| Tür |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| Bilgisayar |Üye bilgisayar adıdır. |
| Grup |Grubun adı. |
| GroupFullName |Kaynak ve kaynak adı dahil olmak üzere Grup tam yolu. |
| GroupSource |Bu grup kaynak gelen toplanan oluştu. <br><br>Active Directory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |Grup toplandığı kaynağının adı.  Active Directory'de, bu etki alanı adıdır. |
| ManagementGroupName |SCOM aracıları için yönetim grubunun adı.  Diğer aracılar için AOI - budur\<çalışma alanı kimliği\> |
| TimeGenerated |Tarih ve saat bilgisayar grubu oluşturulurken veya güncelleştirilirken. |

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) veri kaynakları ve çözümleri toplanan verileri çözümlemek için.  

