---
title: "Azure günlük analizi ve hello OMS portalında aaaManage çalışma | Microsoft Docs"
description: "Çalışma alanları Azure günlük analizi ve hello OMS portalında kullanıcılar, hesaplar, çalışma alanları ve Azure hesapları çeşitli yönetim görevlerini kullanarak yönetebilirsiniz."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/06/2017
ms.author: magoedte
ms.openlocfilehash: 570e6c1f13ad28f120ecd65052d00c4ca986ac98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-workspaces"></a>Çalışma alanlarını yönetme

toomanage erişim tooLog Analytics, çeşitli yönetim görevlerini ilgili tooworkspaces gerçekleştirin. Bu makale, en iyi uygulama önerileri ve yordamları toomanage çalışma alanları sağlar. Bir çalışma alanı, hesap bilgilerini ve hello hesap için basit yapılandırma bilgilerini içeren aslında bir kapsayıcıdır. Siz veya kuruluşunuzun diğer üyeleri birden çok çalışma alanları toomanage farklı tümünden toplanan veri kümelerinin veya BT altyapınızın bölümlerini kullanabilir.

toocreate bir çalışma alanı, şunları yapmanız gerekir:

1. Bir Azure aboneliğine sahip olmanız.
2. Bir çalışma alanı adı seçmeniz.
3. Merhaba çalışma aboneliğinizle ilişkilendirin.
4. Coğrafi bir konum seçmeniz.

## <a name="determine-hello-number-of-workspaces-you-need"></a>Gereksinim duyduğunuz çalışma alanları Hello sayısını belirleyin
Bir çalışma alanı Azure bir kaynaktır ve burada veri toplanan, bir araya getirilir, analiz ve hello Azure portal sunulan bir kapsayıcıdır.

Azure abonelik başına birden çok çalışma olabilir ve bir çalışma alanından daha erişim toomore olabilir. Merhaba sayısını en aza çalışma alanları tooquery sağlar ve bu olası tooquery birden çok çalışma alanları arasında olmadığından arasında hello çoğu verilerin bağıntısını. Bu bölümde, ne zaman, bir çalışma alanında birden çok yararlı toocreate olabilir açıklanmaktadır.

Günümüzde bir çalışma alanı aşağıdakileri sağlar:

* Veri depolama için coğrafi bir konum
* Fatura için ayrıntı düzeyi
* Veri yalıtımı
* Yapılandırma kapsamı

Özellikleri önceki hello üzerinde bağlı olarak, aşağıdakiler toocreate birden çok çalışma durumunda isteyebilirsiniz.

* Global bir şirketseniz ve veri bağımsızlığı veya uyumluluk nedenleriyle verilerin belirli bölgelerde depolanmasına gerek duyuyorsanız.
* Azure kullanıyorsanız ve tooavoid giden veri aktarımı istediğiniz Azure kaynakları yönettiği hello gibi bir çalışma alanı sahip ücretleri hello aynı bölgede.
* Tooallocate ücretleri toodifferent Departmanlar veya kullanıcıların kullanımına bağlı iş grupları istiyor. Her bölüm veya iş grubu için bir çalışma alanı oluşturduğunuzda, Azure fatura ve kullanım deyiminizde hello ücretleri her çalışma alanı için ayrı olarak gösterir.
* Yönetilen hizmet sağlayıcıları ve diğer Müşteri'nin verilerden yalıtılmış yönettiğiniz her müşteri için tookeep hello log analytics verisi gerekir.
* Birden çok müşteriyi yönetmek ve her bir müşteri istediğiniz / bölüm / iş grubunda toosee kendi veri ancak hello verileri değil başkaları için.

Aracıları toocollect verileri kullanarak şunları yapabilirsiniz [her aracı tooreport tooone ya da daha fazla çalışma alanları yapılandırın](log-analytics-windows-agents.md).

System Center Operations Manager'ı kullanıyorsanız her bir Operations Manager yönetim grubu yalnızca bir çalışma alanıyla bağlantılı olabilir. Operations Manager tarafından yönetilen bilgisayarlarda hello Microsoft izleme aracısı yükleyin ve hello Aracısı rapor tooboth Operations Manager ve farklı bir günlük analizi çalışma alanı vardır.

### <a name="workspace-information"></a>Çalışma alanı bilgileri

Hello Azure portal alanınızdaki ilgili ayrıntıları görüntüleyebilirsiniz. Merhaba OMS portalında ayrıntıları da görüntüleyebilirsiniz.

#### <a name="view-workspace-information-in-hello-azure-portal"></a>Hello Azure portal'ın çalışma bilgilerini görüntüleme

1. Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com) Azure aboneliğinizi kullanarak.
2. Merhaba üzerinde **Hub** menüsünde tıklatın **daha fazla hizmet** ve kaynakları hello listesinde yazın **günlük analizi**. Yazmaya başladığınızda liste filtreleri, girişinize göre hello. **Log Analytics**’i tıklayın.  
    ![Azure hub'ı](./media/log-analytics-manage-access/hub.png)  
3. Merhaba günlük analizi abonelikleri dikey penceresinde, bir çalışma alanı seçin.
4. Merhaba çalışma dikey penceresinde hello çalışma ve ek bilgi için bağlantılar hakkındaki ayrıntıları görüntüler.  
    ![çalışma alanı ayrıntıları](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>Hesapları ve kullanıcıları yönetme
Her çalışma kendisiyle ilişkili birden fazla hesap olabilir ve her hesabın (Microsoft hesabı veya Kurumsal hesap) erişim toomultiple çalışma alanları olabilir.

Varsayılan olarak, hello hello çalışma alanının yönetici hello Microsoft hesabı veya hello çalışma alanı oluşturur kuruluş hesabı haline gelir.

Erişim tooa günlük analizi çalışma alanı denetleyen iki izni modeli vardır:

1. Eski Log Analytics kullanıcı rolleri
2. [Azure rol tabanlı erişim](../active-directory/role-based-access-control-configure.md)

Aşağıdaki tablonun hello her izni modeli kullanılarak ayarlanabilir hello erişim özetlenmektedir:

|                          | Log Analytics portalı | Azure portalına | API (PowerShell dahil) |
|--------------------------|----------------------|--------------|----------------------------|
| Log Analytics kullanıcı rolleri | Evet                  | Hayır           | Hayır                         |
| Azure rol tabanlı erişim  | Evet                  | Evet          | Evet                        |

> [!NOTE]
> Günlük analizi hello günlük analizi kullanıcı rollerini değiştirme hello izinler modeli toouse Azure rol tabanlı erişim taşımaktır.
>
>

Merhaba eski günlük analizi kullanıcı rolleri yalnızca hello gerçekleştirilen erişim tooactivities kontrol [günlük analizi portalında](https://mms.microsoft.com).

Etkinlikler de aşağıdaki hello Azure izinleri gerektirir:

| Eylem                                                          | Gereken Azure İzni | Notlar |
|-----------------------------------------------------------------|--------------------------|-------|
| Yönetim çözümlerini ekleme ve kaldırma                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| Fiyatlandırma katmanı hello değiştirme                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| Hello verileri görüntüleme *yedekleme* ve *Site Recovery* çözüm döşeme | Yönetici / Ortak yönetici | Erişimleri kaynakları hello Klasik dağıtım modeli kullanılarak dağıtılabilir |
| Hello Azure portalında bir çalışma alanı oluşturma                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-toolog-analytics-using-azure-permissions"></a>Erişim tooLog Analytics yönetme Azure izinlerini kullanma
Azure izinleri kullanarak toogrant erişim toohello günlük analizi çalışma alanı izleyin hello adımlarda [rol atamalarını toomanage erişim tooyour Azure abonelik kaynaklarını kullanmak](../active-directory/role-based-access-control-configure.md).

Azure Log Analytics için iki yerleşik kullanıcı rolüne sahiptir:
- Log Analytics Okuyucusu
- Log Analytics Katkıda Bulunan

Merhaba üyeleri *günlük analizi okuyucu* rol kullanabilirsiniz:
- Tüm izleme verilerini görüntüleme ve arama 
- Tüm Azure kaynakları üzerinde Azure tanılama Hello yapılandırmasını görüntüleme dahil olmak üzere, izleme ayarlarını görüntüleyin.

| Tür    | İzin | Açıklama |
| ------- | ---------- | ----------- |
| Eylem | `*/read`   | Özelliği tooview tüm kaynaklar ve kaynak yapılandırması. Aşağıdakileri görüntülemeyi içerir: <br> Sanal makine uzantısı durumu <br> Kaynaklarda Azure tanılamalarının yapılandırması <br> Tüm kaynakların tüm özellikleri ve ayarları |
| Eylem | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | Özelliği tooperform günlük arama v2 sorguları |
| Eylem | `Microsoft.OperationalInsights/workspaces/search/action` | Özelliği tooperform günlük arama v1 sorguları |
| Eylem | `Microsoft.Support/*` | Özelliği tooopen destek çalışmaları |
|Eylem Dışı | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | API ve tooinstall çalışma alanı anahtarı gerekli toouse hello veri toplama aracılarını okuma engeller |


Merhaba üyeleri *günlük analizi katkıda bulunan* rol kullanabilirsiniz:
- Tüm izleme verilerini okuma 
- Otomasyon hesaplarını oluşturma ve yapılandırma
- Yönetim çözümlerini ekleme ve kaldırma
- Depolama hesabı anahtarlarını okuma 
- Azure Depolama’dan günlüklerin toplanmasını yapılandırma
- Azure kaynaklarına ilişkin izleme ayarlarını düzenleme:
  - Merhaba VM uzantısı tooVMs ekleme
  - Tüm Azure kaynaklarında Azure tanılamayı yapılandırma

> [!NOTE] 
> Merhaba özelliği tooadd bir sanal makine uzantısı tooa sanal makine toogain üzerinde tam denetim bir sanal makine kullanabilirsiniz.

| İzin | Açıklama |
| ---------- | ----------- |
| `*/read`     | Özelliği tooview tüm kaynaklar ve kaynak yapılandırması. Aşağıdakileri görüntülemeyi içerir: <br> Sanal makine uzantısı durumu <br> Kaynaklarda Azure tanılamalarının yapılandırması <br> Tüm kaynakların tüm özellikleri ve ayarları |
| `Microsoft.Automation/automationAccounts/*` | Özelliği toocreate ekleme ve runbook'ları düzenleme dahil olmak üzere Azure Automation hesapları ve yapılandırma |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | Ekle, Güncelleştir ve hello Microsoft İzleme Aracısı uzantısı ve hello OMS Aracısı Linux uzantısı dahil olmak üzere, sanal makine uzantıları Kaldır |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | Görünüm hello depolama hesabı anahtarı. Azure depolama hesapları arasından tooconfigure günlük analizi tooread günlükleri gerekli |
| `Microsoft.Insights/alertRules/*` | Uyarı kurallarını ekleme, güncelleştirme ve kaldırma |
| `Microsoft.Insights/diagnosticSettings/*` | Azure kaynaklarında tanılama ayarlarını ekleme, güncelleştirme ve kaldırma |
| `Microsoft.OperationalInsights/*` | Log Analytics çalışma alanları için yapılandırmaları ekleme, güncelleştirme ve kaldırma |
| `Microsoft.OperationsManagement/*` | Yönetim çözümlerini ekleme ve kaldırma |
| `Microsoft.Resources/deployments/*` | Dağıtımları oluşturma ve silme. Çözümleri, çalışma alanlarını ve otomasyon hesaplarını eklemek ve kaldırmak için gereklidir |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | Dağıtımları oluşturma ve silme. Çözümleri, çalışma alanlarını ve otomasyon hesaplarını eklemek ve kaldırmak için gereklidir |

tooadd ekleme ve kaldırma kullanıcılar tooa kullanıcı rolü, gerekli toohave `Microsoft.Authorization/*/Delete` ve `Microsoft.Authorization/*/Write` izni.

Bu rolleri toogive kullanıcılara erişim farklı kapsamların kullanın:
- Abonelik - hello Abonelikteki erişim tooall çalışma alanları
- Kaynak grubu - hello kaynak grubunda erişim tooall çalışma
- Kaynak - erişim tooonly hello çalışma alanı belirtildi

Kullanım [özel roller](../active-directory/role-based-access-control-custom-roles.md) toocreate rolleri hello özel izinler gerekli.

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Azure kullanıcı rolleri ve Log Analytics portalı kullanıcı rolleri
Konumundaki varsa, en az Azure okuma izni hello günlük analizi çalışma alanındaki, hello tıklayarak hello günlük analizi portalında açabilirsiniz **OMS portalı** hello günlük analizi çalışma alanı görüntülenirken görev.

Merhaba günlük analizi portalında açarken toousing hello eski günlük analizi kullanıcı rolleri geçin. Bir rol ataması hello günlük analizi portalında yoksa hizmet hello [denetimleri hello hello çalışma alanı'na sahip Azure izinleri](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource).
Rol atamalarınızı hello günlük analizi portalında gibi kullanılarak belirlenir:

| Koşullar                                                   | Atanan Log Analytics kullanıcı rolü | Notlar |
|--------------------------------------------------------------|----------------------------------|-------|
| Hesabınızı tooa eski günlük analizi kullanıcı rolüne ait     | Günlük analizi kullanıcı rolü Hello belirtilen | |
| Hesabınızı tooa eski günlük analizi kullanıcı rolüne ait değil <br> Tam Azure izinleri toohello çalışma (`*` izin <sup>1</sup>) | Yönetici ||
| Hesabınızı tooa eski günlük analizi kullanıcı rolüne ait değil <br> Tam Azure izinleri toohello çalışma (`*` izin <sup>1</sup>) <br> `Microsoft.Authorization/*/Delete` ve `Microsoft.Authorization/*/Write` *eylemleri değil* | Katılımcı ||
| Hesabınızı tooa eski günlük analizi kullanıcı rolüne ait değil <br> Azure okuma izni | Salt Okunur ||
| Hesabınızı tooa eski günlük analizi kullanıcı rolüne ait değil <br> Azure izinleri anlaşılmadı | Salt Okunur ||
| Bulut Çözümü Sağlayıcısı (CSP) tarafından yönetilen abonelikler için <br> oturum açma ile Merhaba hello bağlı Azure Active Directory toohello çalışma alanında hesabıdır | Yönetici | Genellikle hello müşterinin bir CSP |
| Bulut Çözümü Sağlayıcısı (CSP) tarafından yönetilen abonelikler için <br> oturum açma ile Merhaba hesabı hello bağlı Azure Active Directory toohello çalışma alanında değil | Katılımcı | Genellikle hello CSP |

<sup>1</sup> çok başvuran[Azure izinleri](../active-directory/role-based-access-control-custom-roles.md) rol tanımları hakkında daha fazla bilgi için. Roller, bir eyleme değerlendirirken `*` çok eşdeğer olmayan`Microsoft.OperationalInsights/workspaces/*`.

Bazı noktaları tookeep hello Azure portal hakkında unutmayın:

* Http://mms.microsoft.com kullanarak toohello OMS portalında oturum açtığınızda hello bkz **bir çalışma alanı seçin** listesi. Bu liste yalnızca bir Log Analytics kullanıcı rolüne sahip olduğunuz çalışma alanlarını içerir. sahip olduğunuz toosee hello çalışma alanları erişim toowith Azure abonelikleri hello URL'SİNİN bir parçası toospecify bir kiracı gerekir. Örneğin:  `mms.microsoft.com/?tenant=contoso.com`. Merhaba Kiracı genellikle toosign içinde kullandığınız hello e-posta adresi son kısmı tanımlayıcısıdır.
* Sahip olduğunuz tooa portalına erişmek doğrudan toousing Azure toonavigate istiyorsanız, izinleri ve ardından hello URL'SİNİN bir parçası toospecify hello kaynak gerekir. Bu olası tooget PowerShell kullanarak bu URL'dir.

  Örneğin, `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`.

  Merhaba URL'si şuna benzer:`https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-hello-oms-portal"></a>Merhaba OMS portalı kullanıcıları yönetme
Kullanıcı ve Grup hello üzerinde yönetmek **kullanıcıları yönetme** hello sekmesinde **hesapları** hello Ayarları sayfası sekmesindedir.   

![Kullanıcıları yönetme](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-tooan-existing-workspace"></a>Bir kullanıcı tooan varolan çalışma Ekle
Adımları tooadd bir kullanıcı veya grup tooa çalışma alanı aşağıdaki hello kullanın.

1. Merhaba OMS portalında hello tıklatın **ayarları** döşeme.
2. Merhaba tıklatın **hesapları** sekmesini ve sonra hello **kullanıcıları yönetme** sekmesi.
3. Merhaba, **kullanıcıları yönetme** bölümünde, hello hesap türü tooadd seçin: **kuruluş hesabı**, **Microsoft Account**, **Microsoft Support**.

   * Microsoft Account seçerseniz, Microsoft Account hello ile ilişkili hello kullanıcı hello e-posta adresini yazın.
   * Kurumsal hesap seçerseniz, hello kullanıcı parçası girin veya grubun adını veya e-posta diğer adını ve kullanıcılar ve gruplar eşleşen listesi açılır kutusunda görüntülenir. Bir kullanıcı veya grup seçin.
   * Microsoft Support toogive Microsoft Support mühendisi veya diğer Microsoft çalışan geçici erişim tooyour çalışma toohelp sorun giderme tekniklerini kullanın.

     > [!NOTE]
     > Merhaba en iyi performans için Active Directory grupları tek bir OMS hesap toothree ile ilişkili hello sayısı sınırı — Yöneticiler, katkıda bulunanlar için diğeri için salt okunur kullanıcılar için bir tane. Daha fazla Grup kullanarak günlük analizi hello performansını etkileyebilir.
     >
     >
4. Kullanıcı veya grup tooadd Hello türünü seçin: **yönetici**, **katkıda bulunan**, veya **salt okunur kullanıcı**.  
5. **Ekle**'ye tıklayın.

   Bir Microsoft hesabı ekliyorsanız, bir davet toojoin hello çalışma sağladığınız toohello e-posta gönderilir. Merhaba kullanıcı hello davet toojoin OMS hello yönergeleri izleyen sonra hello kullanıcı hello çalışma erişebilir.
   Merhaba kullanıcı bir kurumsal hesap ekliyorsanız, günlük analizi hemen erişebilir.  

#### <a name="edit-an-existing-user-type"></a>Mevcut bir kullanıcı türünü düzenleme
Merhaba hesap rolü OMS hesabınızla ilişkili bir kullanıcı için değiştirebilirsiniz. Aşağıdaki rol seçenekleri şu hello vardır:

* *Yönetici*: Kullanıcıları yönetebilir, tüm uyarıları görüntüleyip bu uyarılar üzerinde işlem yapabilir ve sunucu ekleyip kaldırabilir
* *Katkıda Bulunan*: Tüm uyarıları görüntüleyip bu uyarılar üzerinde işlem yapabilir ve sunucu ekleyip kaldırabilir
* *Yalnızca Okuma Erişimi Olan Kullanıcı*: Yalnızca okuma erişimine sahip olarak işaretlenen kullanıcılar şunları yapamaz:

  1. Çözüm ekleme/kaldırma. Merhaba çözüm Galerisi gizlenir.
  2. **Panom** üzerinde kutucuk ekleme/değiştirme/kaldırma.
  3. Görünüm hello **ayarları** sayfaları. Merhaba sayfaları gizlenir.
  4. Merhaba arama görünümü, Powerbı yapılandırma, kayıtlı aramaları ve uyarılar içinde görevleri gizlenir.

#### <a name="tooedit-an-account"></a>tooedit bir hesap
1. Merhaba OMS portalında hello tıklatın **ayarları** döşeme.
2. Merhaba tıklatın **hesapları** sekmesini ve sonra hello **kullanıcıları yönetme** sekmesi.
3. Toochange istediğiniz hello kullanıcı için Hello rol seçin.
4. Merhaba onay iletişim kutusunda tıklatın **Evet**.

### <a name="remove-a-user-from-a-workspace"></a>Çalışma alanından bir kullanıcıyı kaldırma
Adımları tooremove bir kullanıcı çalışma alanından aşağıdaki hello kullanın. Kaldırma hello kullanıcı hello çalışma kapatmaz. Bunun yerine, o kullanıcı hello çalışma arasındaki hello ilişkiyi kaldırır. Bir kullanıcı birden çok çalışma alanı ile ilişkili ise, o kullanıcı tooOMS içinde oturum ve bunların diğer çalışma alanları bakın.

1. Merhaba OMS portalında hello tıklatın **ayarları** döşeme.
2. Merhaba tıklatın **hesapları** sekmesini ve sonra hello **kullanıcıları yönetme** sekmesi.
3. Tıklatın **kaldırmak** tooremove istediğiniz sonraki toohello kullanıcı adı.
4. Merhaba onay iletişim kutusunda tıklatın **Evet**.

### <a name="add-a-group-tooan-existing-workspace"></a>Bir grup tooan varolan çalışma Ekle
1. Önceki bölümde "tooadd kullanıcı tooan mevcut çalışma" hello, 1-4 arası adımları izleyin.
2. **Kullanıcı/Grup Seç** bölümünde **Grup**'u seçin.  
   ![bir grup tooan varolan çalışma Ekle](./media/log-analytics-manage-access/add-group.png)
3. Merhaba görünen ad veya e-posta adresi girin hello grubu için tooadd istersiniz.
4. Merhaba listesi sonuçlarında Hello grubunu seçin ve ardından **Ekle**.

## <a name="link-an-existing-workspace-tooan-azure-subscription"></a>Var olan bir çalışma alanı tooan Azure aboneliği bağlama
26 Eylül 2016'dan sonra oluşturulan tüm çalışma alanları bağlantılı tooan oluşturma zamanında Azure aboneliği olması gerekir. Oturum açtığınızda bu tarihten önce oluşturulan çalışma alanları bağlantılı tooa çalışma olması gerekir. Hello Azure portal ' hello çalışma alanı oluşturduğunuzda veya Azure aboneliği, çalışma tooan bağladığınızda, Azure Active Directory kuruluş hesabınız olarak bağlanır.

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-oms-portal"></a>toolink çalışma tooan hello OMS portalında Azure aboneliği

- Merhaba OMS portalında oturum açın, istendiğinde tooselect bir Azure aboneliği olan. Toolink tooyour çalışma istediğiniz ve ardından hello aboneliği seçin **bağlantı**.  
    ![Azure aboneliğini bağlama](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > toolink bir çalışma alanı, Azure hesabınıza erişim toohello çalışma toolink istediğiniz zaten olmalıdır.  Diğer bir deyişle, tooaccess hello Azure portalında kullandığınız hello hesabı olmalıdır **aynı hello** hello hesabı tooaccess hello çalışma alanını kullanın. Aksi takdirde bkz [kullanıcı tooan mevcut çalışma eklemek](#add-a-user-to-an-existing-workspace).

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-azure-portal"></a>toolink çalışma tooan hello Azure portalında Azure aboneliği
1. Merhaba içine oturum [Azure portal](http://portal.azure.com).
2. **Log Analytics**’e göz atın ve ardından bu seçeneği belirleyin.
3. Mevcut çalışma alanlarınızın listesini görürsünüz. **Ekle**'ye tıklayın.  
   ![çalışma alanlarının listesi](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. **OMS Çalışma Alanı** altında, **Or link existing (Veya var olanı bağla)** seçeneğine tıklayın.  
   ![mevcut olanı bağlama](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. **Gerekli ayarları yapılandır**'a tıklayın.  
   ![gerekli ayarları yapılandırma](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. Merhaba olmayan çalışma alanlarının listesini tooyour Azure hesabı henüz bağlı bakın. Bir çalışma alanı seçin.  
   ![çalışma alanları seçme](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. Gerekirse, aşağıdaki öğelerindeki hello değerlerini değiştirebilirsiniz:
   * Abonelik
   * Kaynak grubu
   * Konum
   * Fiyatlandırma katmanı  
     ![değerleri değiştirme](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. **Tamam** düğmesine tıklayın. Merhaba çalışma bağlantılı tooyour Azure hesabı sunulmuştur.

> [!NOTE]
> Merhaba çalışma görmüyorsanız toolink istediğiniz sonra erişim toohello çalışma hello OMS portalı kullanılarak oluşturulan Azure aboneliğiniz yok.  toogrant erişim toothis hesabı hello OMS portalı, bkz: [kullanıcı tooan mevcut çalışma eklemek](#add-a-user-to-an-existing-workspace).
>
>

## <a name="upgrade-a-workspace-tooa-paid-plan"></a>Plan Ücretli bir çalışma alanı tooa yükseltme
OMS için üç çalışma alanı plan türü mevcuttur: **Ücretsiz**, **Tek Başına** ve **OMS**.  Merhaba üzerinde olduğunda *serbest* planlama, gönderilen gün tooLog Analytics başına veri 500 MB'lık bir sınırı yoktur.  Bu miktar aşarsa, bu sınırı aşan veri toplamadığı, çalışma alanı Ücretli tooa planı tooavoid toochange gerekir. Plan türünüzü istediğiniz zaman değiştirebilirsiniz.  OMS fiyatlandırması hakkında daha fazla bilgi için bkz. [Fiyatlandırma Ayrıntıları](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing).

### <a name="using-entitlements-from-an-oms-subscription"></a>Bir OMS aboneliğinden gelen destek haklarını kullanma
OMS E1, OMS E2 OMS veya System Center için OMS eklenti satın alma gelen toouse hello yetkilendirmeler seçin hello *OMS* OMS günlük analizi planı.

Bir OMS aboneliği satın aldığınızda, hello yetkilendirmeler tooyour Kurumsal Anlaşma eklenir. Bu sözleşme altında oluşturulan tüm Azure aboneliklerinden hello yetkilendirmeler kullanabilirsiniz. Bu abonelikleri tüm çalışma alanlarına hello OMS yetkilendirmeler kullanın.

bir çalışma alanı kullanımını uygulanan tooyour yetkilendirmeler hello OMS abonelik gelen olduğunu tooensure şunları yapmanız gerekir:

1. Çalışma alanınızı hello hello OMS abonelik Kurumsal Anlaşma parçası olan bir Azure aboneliği oluşturma
2. Select hello *OMS* hello çalışma planlama

> [!NOTE]
> Plan fiyatlandırması, günlük analizi çalışma alanınız 26 Eylül 2016'dan önce oluşturulan ve ise *Premium*, bu çalışma hello OMS eklenti gelen yetkilendirmeler System Center için kullanır. Toohello değiştirerek, yetkilendirmeler kullanabilirsiniz *OMS* fiyatlandırma katmanı.
>
>

Merhaba OMS abonelik yetkilendirmeler hello Azure veya OMS portalında görünür değildir. Yetkilendirmeler ve hello Enterprise Portal kullanımı görebilirsiniz.  

Toochange hello çalışma alanınızı bağlandığı Azure aboneliğine ihtiyacınız varsa, hello Azure PowerShell kullanabileceğiniz [taşıma AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet'i.

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>Kurumsal Anlaşmadaki bir Azure Taahhüdünü Kullanma
Bir OMS aboneliğiniz yoksa, OMS her bir bileşen için ayrı ayrı ödeme ve Azure faturanızda hello kullanım görünür.

Merhaba Kurumsal kayıt toowhich üzerinde Azure parasal taahhüt varsa, Azure aboneliklerinize bağlı olan, günlük analizi kullanımını para yürütme kalan hello karşı otomatik olarak borç.

Toochange gerekiyorsa hello çalışma hello Azure aboneliğine bağlı olduğu, hello Azure PowerShell kullanabileceğiniz [taşıma AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet'i.  

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-azure-portal"></a>Fiyatlandırma katmanı hello Azure portal Ücretli bir çalışma alanı tooa değiştirme
1. Merhaba içine oturum [Azure portal](http://portal.azure.com).
2. **Log Analytics**’e göz atın ve ardından bu seçeneği belirleyin.
3. Mevcut çalışma alanlarınızın listesini görürsünüz. Bir çalışma alanı seçin.  
4. Merhaba çalışma dikey penceresinde, altında **genel**, tıklatın **fiyatlandırma katmanı**.  
5. **Fiyatlandırma katmanı** altında bir fiyatlandırma katmanı seçin ve ardından **Seç**'e tıklayın.  
    ![plan seçme](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. Hello Azure portal görünümünüzde yenilediğinizde, gördüğünüz **fiyatlandırma katmanı** seçtiğiniz hello katmanı için güncelleştirilmiştir.  
    ![güncelleştirilmiş plan](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> Çalışma alanınızı bağlantılı tooan Otomasyon hesabı ise, önce seçebileceğiniz hello *tek başına (başına GB)* fiyatlandırma katmanı herhangi silmelisiniz **otomasyon ve Denetim** çözümleri ve hello Otomasyon bağlantısını Kaldır hesabı. Merhaba çalışma dikey penceresinde, altında **genel**, tıklatın **çözümleri** toosee ve delete çözümler. toounlink hello Otomasyon hesabı hello hello Otomasyon hesabında hello adını tıklatın **fiyatlandırma katmanı** dikey.
>
>

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-oms-portal"></a>Fiyatlandırma katmanı hello OMS portalında Ücretli bir çalışma alanı tooa değiştirme

toochange Merhaba hello OMS portalı kullanarak fiyatlandırma katmanı, bir Azure aboneliğinizin olması gerekir.

1. Merhaba OMS portalında hello tıklatın **ayarları** döşeme.
2. Merhaba tıklatın **hesapları** sekmesini ve sonra hello **Azure aboneliği & veri planı** sekmesi.
3. Fiyatlandırma katmanı toouse istediğiniz hello'ı tıklatın.
4. **Kaydet** düğmesine tıklayın.  
   ![abonelik ve veri planları](./media/log-analytics-manage-access/subscription-tab.png)

Yeni veri planınızı hello OMS portalı Şerit web sayfanızın hello üstünde görüntülenir.

![OMS şeridi](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>Log Analytics'in veri saklama süresini değiştirme

Ücretsiz fiyatlandırma katmanı hello üzerinde günlük analizi veri son yedi gün kullanılabilir hello yapar.
Merhaba standart fiyatlandırma katmanında, günlük analizi veri son 30 gün kullanılabilir hello yapar.
Merhaba Premium fiyatlandırma katmanı olarak, günlük analizi veri son 365 gün kullanılabilir hello yapar.
Merhaba tek başına ve fiyatlandırma katmanları, varsayılan olarak, OMS günlük analizi veri son 31 gün kullanılabilir hello hale getirir.

Merhaba tek başına kullandığınızda ve fiyatlandırma katmanlarına OMS, veri (730 gün) too2 yılda kullanmaya devam edebilir. Merhaba varsayılan 31 gün daha uzun depolanan verilerin veri saklama ücret doğurur. Fiyatlandırma konusunda daha fazla bilgi için bkz. [fazla kullanım ücretleri](https://azure.microsoft.com/pricing/details/log-analytics/).

veri saklama toochange hello uzunluğu:

1. Merhaba içine oturum [Azure portal](http://portal.azure.com).
2. **Log Analytics**’e göz atın ve ardından bu seçeneği belirleyin.
3. Mevcut çalışma alanlarınızın listesini görürsünüz. Bir çalışma alanı seçin.  
4. Merhaba çalışma dikey altında **genel**, tıklatın **bekletme**.  
5. Merhaba kaydırıcı tooincrease kullanın veya gün bekletme hello sayısını azaltın ve ardından **kaydetmek**.  
    ![bekletmeyi değiştirme](./media/log-analytics-manage-access/manage-access-change-retention01.png)

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>Çalışma alanı için Azure Active Directory Kuruluşunu değiştirme

Bir çalışma alanının Azure Active Directory kuruluşunu değiştirebilirsiniz. Değişen hello Azure Active Directory kuruluş tooadd kullanıcılar ve gruplar bu dizin toohello çalışma alanından sağlar.

### <a name="toochange-hello-azure-active-directory-organization-for-a-workspace"></a>bir çalışma alanı için toochange hello Azure Active Directory kuruluş

1. Hello Ayarları sayfasında hello OMS portalında tıklayın **hesapları** ve hello ardından **kullanıcıları yönetme** sekmesi.  
2. Kuruluş hesaplarıyla ilgili hello bilgileri gözden geçirin ve ardından **değişiklik kuruluş**.  
    ![kuruluşu değiştir](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. Azure Active Directory etki alanınızın Merhaba yönetici Hello kimlik bilgilerini girin. Daha sonra çalışma alanınızı bağlantılı tooyour Azure Active Directory etki alanı olduğunu belirten bir bildirim görürsünüz.  
    ![bağlanan çalışma alanı bildirimi](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>Log Analytics çalışma alanını silme
Günlük analizi çalışma alanı sildiğinizde, tüm verileri tooyour çalışma hello OMS hizmetine ' sonraki 30 gün içinde silinir ilgili.

Bir yöneticiyseniz ve hello çalışma alanıyla ilişkilendirilmiş birden çok kullanıcı varsa, bu kullanıcılar ve hello çalışma arasındaki ilişkiyi hello bozuk. Merhaba kullanıcılar diğer çalışma alanları ile ilişkili ise, ardından bunlar OMS bu diğer çalışma alanları ile kullanmaya devam edebilirsiniz. Diğer çalışma alanları ile ilişkili olmayan, ancak ardından toocreate çalışma toouse OMS ihtiyaç duyar.

### <a name="toodelete-a-workspace"></a>toodelete bir çalışma alanı
1. Merhaba içine oturum [Azure portal](http://portal.azure.com).
2. **Log Analytics**’e göz atın ve ardından bu seçeneği belirleyin.
3. Mevcut çalışma alanlarınızın listesini görürsünüz. Merhaba çalışma toodelete istediğinizi seçin.
4. Merhaba çalışma dikey penceresinde tıklayın **silmek**.  
    ![sil](./media/log-analytics-manage-access/delete-workspace01.png)
5. Merhaba delete çalışma onay iletişim kutusunda tıklatın **Evet**.

## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [bağlanmak Windows bilgisayarları tooLog Analytics](log-analytics-windows-agents.md) tooadd aracıları ve veri toplayın.
* [Günlük analizi çözümleri Çözümleri Galerisi hello eklemek](log-analytics-add-solutions.md) tooadd işlevselliği ve toplama verileri.
* [Günlük analizi proxy ve güvenlik duvarı ayarlarını yapılandırma](log-analytics-proxy-firewall.md) kuruluşunuz bir proxy sunucusu veya Güvenlik Duvarı'nı kullanıyorsa aracıları hello günlük analizi hizmeti ile iletişim kurabilmesi için.
