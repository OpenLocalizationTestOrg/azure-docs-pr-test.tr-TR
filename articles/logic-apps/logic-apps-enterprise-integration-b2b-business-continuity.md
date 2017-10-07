---
title: "B2B tümleştirme hesabı - Azure Logic Apps için aaaDisaster kurtarma | Microsoft Docs"
description: "Logic Apps B2B olağanüstü durum kurtarma"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Logic Apps B2B çapraz bölge olağanüstü durum kurtarma

B2B iş yükleri siparişler ve faturalar gibi para işlemleri içerir. Bir olağanüstü sırasında iş düzeyi SLA kendi iş ortaklarıyla üzerinde anlaşmaya varılan bir iş tooquickly kurtarma toomeet hello önemlidir. Bu makalede, toobuild iş sürekliliği planınızı B2B iş yükleri için nasıl gösterilmektedir. 

* Olağanüstü Durum Kurtarma Hazırlık 
* Toosecondary bölge bir olağanüstü durum olay sırasında başarısız oluyor 
* Tooprimary bölge olağanüstü sonra geri dönüş

## <a name="disaster-recovery-readiness"></a>Olağanüstü Durum Kurtarma Hazırlık  

1. Bir ikincil bölge tanımlayabilir ve oluşturabilirsiniz bir [tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) hello ikincil bölge içinde.

2. İş ortakları, şemalar ve burada çalışma durumu hello çoğaltılan toobe toosecondary bölge tümleştirme hesabının gerekir gerekli hello ileti akışları için anlaşmaları ekleyin.

   > [!TIP]
   > Tutarlılık hello tümleştirme hesap yapı'nın Adlandırma kuralında bölgeler arasında olduğundan emin olun. 

3. Merhaba birincil bölgesinden çalışma durumu toopull hello hello ikincil bölge'de bir mantıksal uygulama oluşturun. 

   Bu mantıksal uygulama olmalıdır bir *tetikleyici* ve bir *eylem*. 
   Merhaba tetikleyici tooprimary bölge tümleştirme hesabını bağlaması ve hello eylem toosecondary bölge tümleştirme hesabını bağlaması. 
   Merhaba zaman aralığına dayalı, hello tetikleyici hello çalıştırmak birincil bölge durumu tablosu yoklar ve hello yeni kayıtlar varsa çeker. Merhaba eylem bunları toosecondary bölge tümleştirme hesabını güncelleştirir. 
   Bu, birincil bölge toosecondary bölgesinden tooget artımlı çalışma zamanı durumu yardımcı olur.

4. İş sürekliliği tümleştirme hesabıdır Logic Apps içinde B2B protokolleri - X12, AS2 ve EDIFACT temel toosupport tasarlanmıştır. adımları toofind ayrıntılı, ilgili bağlantıları seçin hello.

5. Merhaba öneri toodeploy ikincil bir bölgede tüm birincil bölge kaynakları çok uzun. 

   Azure SQL Database veya Azure Cosmos DB, Azure Service Bus ve Azure olay hub'ın Mesajlaşma, Azure API Management ve Azure App Service hello Azure Logic Apps özelliği için kullanılan birincil bölge kaynaklar içerir.   

6. Bir birincil bölge tooa ikincil bölge arasında bağlantı kurun. bir birincil bölge durumunu çalıştırmak toopull hello ikincil bir bölgede bir mantıksal uygulama oluşturun. 

   Merhaba mantıksal uygulama tetikleyici ve eylem olması gerekir. 
   Merhaba tetikleyici tooa birincil bölge tümleştirme hesabını bağlanmanız gerekir. 
   Merhaba eylem tooa ikincil bölge tümleştirme hesabını bağlanmanız gerekir. 
   Merhaba zaman aralığına dayalı, hello tetikleyici hello çalıştırmak birincil bölge durumu tablosu yoklar ve hello yeni kayıtlar varsa çeker. 
   Merhaba eylem bunları tooa ikincil bölge tümleştirme hesabını güncelleştirir. 
   Bu işlem tooget artımlı çalışma zamanı durumu hello birincil bölge toohello ikincil bölge ' yardımcı olur.

Logic Apps tümleştirme hesabında iş sürekliliği hello B2B protokolleri X12, AS2 ve EDIFACT göre desteği sağlar. X12 ve AS2 kullanma hakkında ayrıntılı adımlar için bkz: [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) ve [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) bu makalede.

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>Tooa ikincil bölge bir olağanüstü durum olay sırasında başarısız oluyor

Olağanüstü durum olay sırasında iş sürekliliği, doğrudan trafiği toohello ikincil bölge Hello birincil bölge bulunmaması durumunda. Bir iş toorecover hızla RPO'ya/RTO'ya anlaşmaya varılan toomeet hello ortakları tarafından işlevleri ikincil bölge yardımcı olur. Bu ayrıca çaba toofail üzerinden bir bölge tooanother bölgesinden en aza indirir. 

Bir birincil bölge tooa ikincil bölge ' denetim numaraları kopyalanırken beklenen bir gecikme süresi yok. Yinelenen oluşturulan denetim gönderme tooavoid sırasında bir olağanüstü toopartners sayılar, hello öneri tooincrement hello denetim numaraları hello ikincil bölge sözleşmelerde kullanarak [PowerShell cmdlet'leri](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>Geri dönüş tooa birincil bölge sonrası olağanüstü

mevcut olduğunda toofall geri tooa birincil bölge şu adımları izleyin:

1. Merhaba ikincil bölge'de ortakları gelen iletileri kabul durdurun.  

2. Artır tüm hello birincil bölge anlaşmalar için oluşturulan hello denetim numaraları kullanarak [PowerShell cmdlet'leri](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).  

3. Merhaba ikincil bölge toohello birincil bölge doğrudan trafiğinden.

4. Çalışma durumu hello birincil bölgesinden çekmek için hello ikincil bölgede oluşturulan bu hello mantıksal uygulama etkinleştirildiğinden emin olun.

## <a name="x12"></a>X12 

EDI iş sürekliliği X 12 belgeler üzerinde denetim numaraları dayanır:

> [!TIP]
> Merhaba de kullanabilirsiniz [X12 hızlı başlatma şablonunu](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate mantıksal uygulamalar. Oluşturma birincil ve ikincil tümleştirme Önkoşullar toouse hello şablon hesaplarıdır. Merhaba şablonu toocreate iki logic apps, alınan denetim numaraları için bir ve oluşturulan denetim numaraları için başka bir yardımcı olur. İlgili tetikleyiciler ve Eylemler hello tetikleyici toohello birincil tümleştirme hesabı ve hello eylem toohello ikincil tümleştirme hesabı bağlanma hello logic apps içinde oluşturulur.

**Önkoşullar**

gelen iletiler için tooenable olağanüstü durum kurtarma hello X12 anlaşmanın alma ayarlarında hello yinelenen onay ayarlarını seçin.

![Yinelenen onay ayarlarını Seç](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. Oluşturma bir [mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md) ikincil bir bölgede.    

2. Arama **X12**seçip **bir denetim numarasını değiştirildiğinde X12-**.   

   ![X12 arayın](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   Merhaba tetikleyici bağlantı tooan tümleştirme hesabı tooestablish ister. 
   Merhaba tetikleyici olmalıdır bağlı tooa birincil bölge tümleştirme hesabı.

3. Bir bağlantı adı girin, seçin, *birincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.   

   ![Birincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. Merhaba **DateTime toostart denetim sayı eşitleme** ayardır isteğe bağlıdır. Merhaba **sıklığı** çok ayarlanabilir**gün**, **saat**, **Minute**, veya **ikinci** bir aralık ile.   

   ![DateTime ve sıklığı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. Seçin **yeni adım** > **Eylem Ekle**.

   ![Yeni adım, bir eylem Ekle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. Arama **X12**seçip **X12-ekleme veya güncelleştirme denetim numaraları**.   

   ![Ekleyin veya denetim numaraları güncelleştirin](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. tooconnect bir eylem tooa ikincil bölge tümleştirme hesabı seçin **değiştirmek bağlantı** > **yeni bağlantı ekleme** hello kullanılabilir tümleştirme hesapları listesi. Bir bağlantı adı girin, seçin, *ikincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**. 

   ![İkincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. Tooraw girişleri sağ üst köşesinde hello simgesine tıklayarak geçin.

   ![Anahtar tooraw girişleri](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. Gövde hello dinamik içerik seçiciden seçin ve hello mantıksal uygulama kaydedin.

   ![Dinamik içerik alanları](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   Merhaba zaman aralığına dayalı, hello tetikleyici hello alınan birincil bölge denetim sayı tablosunu yoklar ve hello yeni kayıtlar çeker. 
   Hello eylemin hello ikincil bölge tümleştirme hesabındaki hello kayıtlarını güncelleştirir. 
   Herhangi bir güncelleştirme varsa, hello tetikleyici durum olarak görünür **Atlanan**.   

   ![Denetim sayı tablosu](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Merhaba zaman aralığında, bir birincil bölge tooa ikincil bölge ' hello artımlı çalışma zamanı durumu çoğaltır. Olağanüstü durum olay sırasında iş sürekliliği için kullanılabilir, doğrudan trafiğini toohello ikincil bölge Hello birincil bölge değilse. 

## <a name="edifact"></a>EDIFACT 

İş sürekliliği EDI EDIFACT belgeler için Denetim numaralarında temel alır.

**Önkoşullar**

tooenable olağanüstü durum kurtarma gelen iletiler için EDIFACT anlaşmanızın alma ayarlarında hello yinelenen onay ayarlarını seçin.

![Yinelenen onay ayarlarını Seç](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. Oluşturma bir [mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md) ikincil bir bölgede.    

2. Arama **EDIFACT**seçip **bir denetim numarasını değiştirildiğinde EDIFACT -**.

   ![EDIFACT arayın](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   Merhaba tetikleyici bağlantı tooan tümleştirme hesabı tooestablish ister. 
   Merhaba tetikleyici olmalıdır bağlı tooa birincil bölge tümleştirme hesabı. 

3. Bir bağlantı adı girin, seçin, *birincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.    

   ![Birincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. Merhaba **DateTime toostart denetim sayı eşitleme** ayardır isteğe bağlıdır. Merhaba **sıklığı** çok ayarlanabilir**gün**, **saat**, **Minute**, veya **ikinci** bir aralık ile.    

   ![DateTime ve sıklığı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. Seçin **yeni adım** > **Eylem Ekle**.    

   ![Yeni adım, bir eylem Ekle](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. Arama **EDIFACT**seçip **EDIFACT - ekleme veya güncelleştirme denetim numaraları**.   

   ![Ekleyin veya denetim numaraları güncelleştirin](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. tooconnect bir eylem tooa ikincil bölge tümleştirme hesabı seçin **değiştirmek bağlantı** > **yeni bağlantı ekleme** hello kullanılabilir tümleştirme hesapları listesi. Bir bağlantı adı girin, seçin, *ikincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.

   ![İkincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. Tooraw girişleri sağ üst köşesinde hello simgesine tıklayarak geçin.

   ![Anahtar tooraw girişleri](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. Gövde hello dinamik içerik seçiciden seçin ve hello mantıksal uygulama kaydedin.   

   ![Dinamik içerik alanları](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   Merhaba zaman aralığına dayalı, hello tetikleyici hello alınan birincil bölge denetim sayı tablosunu yoklar ve hello yeni kayıtlar çeker.
   Merhaba eylemin hello kayıtları toohello ikincil bölge tümleştirme hesabını güncelleştirir. 
   Herhangi bir güncelleştirme varsa, hello tetikleyici durum olarak görünür **Atlanan**.

   ![Denetim sayı tablosu](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Merhaba zaman aralığında, bir birincil bölge tooa ikincil bölge ' hello artımlı çalışma zamanı durumu çoğaltır. Olağanüstü durum olay sırasında iş sürekliliği için kullanılabilir, doğrudan trafiğini toohello ikincil bölge Hello birincil bölge değilse. 

## <a name="as2"></a>AS2 

İş sürekliliği hello AS2 protokolünü kullanan belgeler için hello ileti kimliği ve hello MIC değeri temel alır.

> [!TIP]
> Merhaba de kullanabilirsiniz [AS2 Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate mantıksal uygulamalar. Oluşturma birincil ve ikincil tümleştirme Önkoşullar toouse hello şablon hesaplarıdır. Merhaba şablonu bir tetikleyici ve eylem sahip bir mantıksal uygulama oluşturma yardımcı olur. Merhaba mantıksal uygulama, bir tetikleyici tooa birincil tümleştirme hesabı ve eylem tooa ikincil tümleştirme hesabı bir bağlantı oluşturur.

1. Oluşturma bir [mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md) hello ikincil bölge içinde.  

2. Arama **AS2**seçip **AS2 - olduğunda bir MIC değer oluşturulur**.   

   ![AS2 arayın](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   Bir tetikleyici tooestablish bağlantı tooan tümleştirme hesabı ister. 
   Merhaba tetikleyici olmalıdır bağlı tooa birincil bölge tümleştirme hesabı. 
   
3. Bir bağlantı adı girin, seçin, *birincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.

   ![Birincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. Merhaba **DateTime toostart MIC değer eşitleme** ayardır isteğe bağlıdır. Merhaba **sıklığı** çok ayarlanabilir**gün**, **saat**, **Minute**, veya **ikinci** bir aralık ile.   

   ![DateTime ve sıklığı](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. Seçin **yeni adım** > **Eylem Ekle**.  

   ![Yeni adım, bir eylem Ekle](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. Arama **AS2**seçip **AS2 - MIC içeriği güncelleştirmek ya da eklemek**.  

   ![MIC ekleme veya güncelleştirme](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. tooconnect bir eylem tooa ikincil tümleştirme hesabı seçin **değiştirmek bağlantı** > **yeni bağlantı ekleme** hello kullanılabilir tümleştirme hesapları listesi. Bir bağlantı adı girin, seçin, *ikincil bölge tümleştirme hesabını* hello gelen listelemek ve seçin **oluşturma**.

   ![İkincil bölge tümleştirme hesap adı](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. Tooraw girişleri sağ üst köşesinde hello simgesine tıklayarak geçin.

   ![Anahtar tooraw girişleri](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. Gövde hello dinamik içerik seçiciden seçin ve hello mantıksal uygulama kaydedin.   

   ![Dinamik içerik](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   Merhaba zaman aralığına dayalı, hello tetikleyici hello birincil bölge tablo yoklar ve hello yeni kayıtlar çeker. Merhaba eylem bunları toohello ikincil bölge tümleştirme hesabını güncelleştirir. 
   Herhangi bir güncelleştirme varsa, hello tetikleyici durum olarak görünür **Atlanan**.  

   ![Birincil bölge tablosu](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

Merhaba zaman aralığına dayalı, hello artımlı çalışma zamanı durumu hello birincil bölge toohello ikincil bölge ' çoğaltır. Olağanüstü durum olay sırasında iş sürekliliği için kullanılabilir, doğrudan trafiğini toohello ikincil bölge Hello birincil bölge değilse. 

## <a name="next-steps"></a>Sonraki adımlar

[B2B iletilerini izleme](logic-apps-monitor-b2b-message.md)

