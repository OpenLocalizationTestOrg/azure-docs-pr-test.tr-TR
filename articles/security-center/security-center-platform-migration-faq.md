---
title: "aaaSecurity merkezi platformu geçiş ile ilgili SSS | Microsoft Docs"
description: "Bu SSS hello Azure Güvenlik Merkezi platformu geçiş hakkında sorular yanıtlanmaktadır."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>Güvenlik Merkezi platformu geçiş ile ilgili SSS
Erken Haziran 2017 içinde hello Microsoft İzleme Aracısı toocollect ve deposu verileri kullanarak Azure Güvenlik Merkezi başlamıştır. toolearn daha, fazla [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md). Bu SSS hello platform geçişi hakkında sorular yanıtlanmaktadır.

## <a name="data-collection-agents-and-workspaces"></a>Veri toplama, aracıları ve çalışma alanları

### <a name="how-is-data-collected"></a>Verileri nasıl toplanır?
Güvenlik Merkezi, hello Microsoft İzleme Aracısı toocollect güvenlik Vm'leriniz verilerden kullanır. Merhaba güvenlik verileri kullanılan tooidentify güvenlik açıkları olan güvenlik yapılandırmalarını ve kullanılan toodetect tehdit güvenlik olayları hakkında bilgiler içerir. Merhaba aracısı tarafından toplanan verileri var olan bir günlük analizi çalışma alanı bağlı toohello VM veya Güvenlik Merkezi tarafından oluşturulan yeni bir çalışma alanı depolanır. Güvenlik Merkezi, yeni bir çalışma alanı oluşturduğunda, hello coğrafi konuma Merhaba, VM dikkate alınır.

> [!NOTE]
> Merhaba Microsoft izleme aracısı aynı aracı kullanılan hello hello Operations Management Suite (OMS), günlük analizi hizmeti ve System Center Operations Manager (SCOM) olur.
>
>

Veri toplama hello için ilk kez veya aboneliklerinizi geçirildiğinde etkinleştirilmişse, Güvenlik Merkezi hello Microsoft İzleme Aracısı zaten bir Azure uzantısı, VM'lerin her birinde'yüklüyse toosee denetler. Merhaba Microsoft izleme aracısı yüklü değilse, Güvenlik Merkezi olur:

- Merhaba VM üzerinde Hello Microsoft Monitoring aracısı yükleyin
   - Güvenlik Merkezi tarafından önceden oluşturulmuş bir çalışma alanı aynı coğrafi konuma VM hello gibi hello hello varsa aracısıdır bağlı toothis çalışma
   - bir çalışma alanı mevcut değilse, Güvenlik Merkezi yeni bir kaynak grubu oluşturur ve çalışma alanında, coğrafi konuma varsayılan ve hello Aracısı toothat çalışma bağlayın. Merhaba çalışma ve kaynak grubu için adlandırma kuralı Hello şunlardır:

       Çalışma alanı: DefaultWorkspace-[abonelik kimliği]-[coğrafi]

       Kaynak grubu: DefaultResouceGroup-[coğrafi]
- Güvenlik Merkezi çözüm hello çalışma alanı'na yükleme

Merhaba çalışma Hello konumunu hello VM hello konumunu temel alır. toolearn daha, fazla [veri güvenliği](security-center-data-security.md).

> [!NOTE]
> Önceki tooplatform geçiş, Güvenlik Merkezi güvenlik verileri hello Azure Monitoring Agent kullanarak Vm'leriniz toplanır ve veri depolama hesabında depolanır. Merhaba platform geçişten sonra çalışma alanı toocollect ve deposu aynı veri hello ve Güvenlik Merkezi hello Microsoft İzleme Aracısı kullanır. Merhaba depolama hesabı hello geçişten sonra kaldırılabilir.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>Günlük analizi veya Güvenlik Merkezi tarafından oluşturulan hello çalışma alanları üzerindeki OMS faturalandırılır 'M?
Hayır. Güvenlik Merkezi tarafından oluşturulan çalışma alanları için OMS düğümü faturalama başına yapılandırılmış olsa OMS ücretlendirme değil. Güvenlik Merkezi faturalama her zaman bir çalışma alanı'na yüklü Güvenlik Merkezi güvenlik ilkesi ve hello çözümlerinizi dayanır:

- **Ücretsiz katmanı** – Güvenlik Merkezi hello 'SecurityCenterFree' çözüm hello varsayılan çalışma alanı'na yükler. Merhaba ücretsiz katmanına faturalandırılır değil.
- **Standart katmanı** – Güvenlik Merkezi yükler hello 'SecurityCenterFree' ve 'Security' çözümlerini hello varsayılan çalışma alanı.

Fiyatlandırma hakkında daha fazla bilgi için bkz: [Güvenlik Merkezi fiyatlandırma](https://azure.microsoft.com/pricing/details/security-center/). Fiyatlandırma sayfası adresleri hello toosecurity veri depolama ve eşit olarak bölünmüş fatura Haziran 2017 başlayarak değiştirir.

> [!NOTE]
> Güvenlik Merkezi tarafından oluşturulan çalışma alanlarının Hello OMS fiyatlandırma katmanı Güvenlik Merkezi faturalama etkilemez.
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>Güvenlik Merkezi tarafından oluşturulan hello varsayılan çalışma alanları silebilmek için?
**Merhaba varsayılan çalışma alanı siliniyor önerilmez.** Güvenlik Merkezi, hello varsayılan çalışma alanları toostore güvenlik verileri, sanal makineleri kullanır.  Bir çalışma alanı, Güvenlik Merkezi silerseniz oluşturulamıyor toocollect bu verileri ve bazı güvenlik önerileri ve uyarılar kullanılamıyor

toorecover, Kaldır hello Microsoft Monitoring Agent'hello VM'ler silinmiş bağlı toohello çalışma. Güvenlik Merkezi hello aracısı yeniden yükler ve yeni varsayılan çalışma alanı oluşturur.

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>Ne hello Microsoft İzleme Aracısı hello VM üzerinde bir uzantısı olarak zaten yüklendi mi?
Güvenlik Merkezi, varolan bağlantılar toouser çalışma kılmaz. Güvenlik Merkezi depoları güvenlik hello hello çalışma alanında VM verilerden zaten bağlı.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>Ne ı hello makinede ancak uzantı olarak değil yüklü Microsoft İzleme Aracısı oldu?
Merhaba Microsoft İzleme Aracısı doğrudan yüklüyse hello üzerinde VM (olarak değil bir Azure uzantısı), Güvenlik Merkezi hello Microsoft İzleme Aracısı yüklenmez ve güvenlik izleme sınırlı olacaktır.

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>Bu uzantılar kaldırmanın hello etkisi nedir?
Microsoft Monitoring uzantısı hello kaldırırsanız, Güvenlik Merkezi değil hello VM mümkün toocollect güvenlik verilerini ve bazı güvenlik önerileri ve uyarılar kullanılamaz. 24 saat içinde Güvenlik Merkezi hello VM hello uzantısı eksik ve yeniden yükler uzantısı hello belirler.

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>Nasıl ı hello otomatik aracı yükleme ve çalışma alanı oluşturmayı durdur?
Aboneliklerinizi hello güvenlik ilkesi için veri toplamayı devre dışı bırakabilir, ancak bu önerilmez. Veri toplama sınırları Güvenlik Merkezi önerileri ve uyarılar kapatma. Veri toplama hello standart fiyatlandırma katmanında abonelikler için gereklidir. toodisable veri toplama:

1. Aboneliğinizi hello standart katmanı için yapılandırdıysanız, bu abonelik için hello Güvenlik İlkesi'ni açın ve seçin hello **serbest** katmanı.

   ![Fiyatlandırma katmanı][1]

2. Ardından, kapatma veri toplamayı devre dışı seçerek **kapalı** hello üzerinde **güvenlik ilkesi – veri toplama** dikey.

   ![Veri toplama][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Güvenlik Merkezi tarafından yüklenen OMS uzantıları nasıl kaldırılsın mı?
Microsoft Monitoring Agent hello el ile kaldırabilirsiniz. Güvenlik Merkezi önerileri ve uyarılar sınırlar bu önerilmez.

> [!NOTE]
> Veri toplama etkinleştirilmişse, Güvenlik Merkezi kaldırdıktan sonra hello aracısı yeniden yükler.  El ile Merhaba Aracısı kaldırmadan önce toodisable veri toplama gerekir. Bkz: [nasıl ı Durdur hello otomatik aracı yükleme ve çalışma alanı oluşturma?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) veri toplamayı devre dışı bırakma hakkında yönergeler için.
>
>

toomanually hello Aracısı kaldırın:

1.  Merhaba Portalı'nda açmak **günlük analizi**.
2.  Merhaba günlük analizi dikey penceresinde, bir çalışma alanı seçin:
3.  Yoksa toomonitor istediğiniz ve seçin, her bir VM seçin **Bağlantıyı Kes**.

   ![Merhaba aracısını Kaldır][3]

> [!NOTE]
> Bir Linux VM uzantısı olmayan OMS Aracısı zaten varsa, hello uzantısını kaldırma hello Aracısı kaldırır ve hello müşterinin tooreinstall onu.
>
>

## <a name="existing-oms-customers"></a>Var olan OMS müşterileri

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>Güvenlik Merkezi, VM'ler ve çalışma alanları arasında var olan tüm bağlantıları devre dışı bırakmaz?
Bir VM hello Azure uzantı olarak yüklü olan Microsoft İzleme Aracısı zaten varsa, Güvenlik Merkezi hello varolan çalışma bağlantı kılmaz. Bunun yerine, Güvenlik Merkezi, hello mevcut çalışma kullanır.

Güvenlik Merkezi çözüm hello çalışma alanı'na yüklü henüz yoksa ve hello çözümdür uygulanan yalnızca toohello ilgili VM'ler. Bir çözümü eklediğinizde, varsayılan tooall Windows ve Linux aracıları bağlı tooyour günlük analizi çalışma alanı tarafından otomatik olarak dağıtılır. [Çözüm hedefleme](../operations-management-suite/operations-management-suite-solution-targeting.md), bir OMS özelliği olduğu verir tooapply kapsam tooyour çözümler.

Microsoft Monitoring Agent Hello doğrudan yüklüyse hello üzerinde VM (olarak değil bir Azure uzantısı), Güvenlik Merkezi hello Microsoft İzleme Aracısı yüklenmez ve güvenlik izleme sınırlıdır.

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>Merhaba veri platformu geçiş Vm'lerimin ve çalışma Alanım biri arasında hello bağlantı ihlal ne yapmam gerekir?
Bu durum oluşmamalıdır. Bu, ardından görülüyorsa [Azure destek isteği oluşturmak](../azure-supportability/how-to-create-azure-support-request.md) ve aşağıdaki ayrıntılara hello içerir:

- VM hello Hello Azure kaynak kimliği etkilenen
- Merhaba bağlantı kesildi önce hello uzantısına göre yapılandırılmış hello çalışma alanının Hello Azure kaynak kimliği
- Merhaba aracısı ve daha önce yüklenen sürüm

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>Güvenlik Merkezi çözümleri my varolan OMS çalışma alanlarına yükler mi? Merhaba fatura etkileri nelerdir?
Ne zaman Güvenlik Merkezi VM zaten bağlı tooa çalışma Güvenlik Merkezi, oluşturduğunuz olduğunu tanımlar. Bu çalışma alanındaki fiyatlandırma katmanı tooyour göre çözümleri sağlar. Merhaba çözümleri aracılığıyla ilgili Azure VM'ler, uygulanan yalnızca toohello olan [çözüm hedefleme](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), hello fatura kalır aynı hello.

- **Ücretsiz katmanı** – Güvenlik Merkezi hello 'SecurityCenterFree' çözüm hello çalışma alanı'na yükler. Merhaba ücretsiz katmanına faturalandırılır değil.
- **Standart katmanı** – Güvenlik Merkezi yükler hello 'SecurityCenterFree' ve 'Security' çözümlerini hello çalışma.

   ![Varsayılan çalışma alanı çözümlerini][4]

> [!NOTE]
> Merhaba 'Security' günlük analizi çözümde hello güvenlik & OMS denetim çözümde biçimindedir.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>Çalışma Alanım ortamda zaten var, bunları toocollect güvenlik verileri kullanabilir miyim?
Bir VM hello Azure uzantı olarak yüklü olan Microsoft İzleme Aracısı zaten varsa, Güvenlik Merkezi hello mevcut bağlı çalışma kullanır. Güvenlik Merkezi çözüm hello çalışma alanı'na yüklü henüz yoksa ve hello çözümdür uygulanan yalnızca toohello yoluyla ilgili VM'ler [çözüm hedefleme](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Güvenlik Merkezi Vm'lerinde hello Microsoft İzleme Aracısı yüklendiğinde, Güvenlik Merkezi tarafından oluşturulan hello varsayılan çalışma alanları kullanır. Müşteriler, hangi çalışma alanları kullanılan mümkün tooconfigure yakında sunulacaktır.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>Zaten bir güvenlik çözümü my çalışma alanlarına var. Merhaba fatura etkileri nelerdir?
Güvenlik ve denetim çözüm Hello Azure VM'ler için Güvenlik Merkezi standart katman özellikleri kullanılan tooenable ' dir. Merhaba güvenlik ve denetim çözümü bir çalışma alanı'na zaten yüklüyse, Güvenlik Merkezi hello mevcut çözümünü kullanır. Faturalama değişiklik yoktur.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba Güvenlik Merkezi platformu geçiş hakkında daha fazla toolearn bakın

- [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md)
- [Azure Güvenlik Merkezi sorun giderme kılavuzu](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
