---
title: "aaaMonitor sanal makine değişiklikleri - Azure olay kılavuz & Logic Apps | Microsoft Docs"
description: "Azure olay kılavuz ve Logic Apps kullanarak sanal makineleri (VM'ler) yapılandırma değişiklikleri denetleyin"
keywords: "Logic apps, olay kılavuzları, sanal makine, VM"
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a>Azure olay kılavuz ve Logic Apps ile sanal makine değişikliklerini izleme

Bir Otomatik Başlat [mantığı uygulama iş akışı](../logic-apps/logic-apps-what-are-logic-apps.md) belirli olaylar olduğunda gerçekleşir Azure kaynakları veya üçüncü taraf kaynakları. Bu kaynaklar bu olayları tooan yayımlayabilirsiniz [Azure olay kılavuz](../event-grid/overview.md). Buna karşılık, sıralar, Web kancalarını, bu olayları toosubscribers hello olay kılavuz iter veya [olay hub'ları](../event-hubs/event-hubs-what-is-event-hubs.md) uç noktalar olarak. Bir abone olarak mantıksal uygulamanızı hello olay kılavuz bu olaylarından otomatik iş akışları tooperform görevler -, herhangi bir kod yazarken çalıştırmadan önce bekleyebilirsiniz.

Örneğin, bazı olaylar yayımcılar toosubscribers hello Azure olay kılavuz hizmeti aracılığıyla gönderebilirsiniz şunlardır:

* Oluşturma, okuma, güncelleştirme veya kaynak silme. Örneğin, Azure aboneliğinizde üzerinde ücretlendirme ve faturanızı etkileyen değişiklikleri izleyebilirsiniz. 
* Ekleyebilir veya bir kişinin Azure aboneliğinden kaldırabilirsiniz.
* Uygulamanızı belirli bir eylemi gerçekleştirir.
* Bir kuyruktaki yeni bir ileti görüntülenir.

Bu öğretici, değişiklikleri tooa sanal makineyi izler ve bu değişiklikleri hakkında e-posta gönderir. bir mantıksal uygulama oluşturur. Bir Azure kaynağı için bir olay aboneliği ile bir mantıksal uygulama oluşturduğunuzda, bir olay kılavuz toohello mantıksal uygulama aracılığıyla bu kaynaktan olayları akışı. Başlangıç Öğreticisi size bu mantıksal uygulama oluşturma sürecinde yardımcı olur:

![Genel Bakış - olay kılavuz ve mantığı uygulama ile yeni bir sanal makine İzleyicisi](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Bir olay kılavuz olayları izler bir mantıksal uygulama oluşturun.
> * Özellikle sanal makine değişiklikleri denetleyen bir koşul ekleyin.
> * Sanal makineniz değiştiğinde e-posta gönderin.

## <a name="prerequisites"></a>Ön koşullar

* Bir e-posta hesabından [Azure mantıksal uygulamaları tarafından desteklenen herhangi bir e-posta sağlayıcısına](../connectors/apis-list.md)Office 365 Outlook, Outlook.com veya bildirim göndermek için Gmail gibi. Bu öğretici, Office 365 Outlook kullanır.

* A [sanal makine](https://azure.microsoft.com/services/virtual-machines). Zaten yapmadıysanız, bir sanal makine üzerinden oluşturmak bir [VM öğretici oluşturma](https://docs.microsoft.com/azure/virtual-machines/). toomake hello sanal makine olayları, yayımlama, [toodo herhangi bir şey başka gerekmeyen](../event-grid/overview.md).

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a>Bir olay kılavuz olayları izler bir mantıksal uygulama oluşturma

İlk olarak, bir mantıksal uygulama oluşturma ve hello kaynak grubu, sanal makine için izleyen olay kılavuz tetikleyicisi ekleyin. 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com). 

2. Merhaba sol üst köşesinin hello ana Azure menüsünün seçin **yeni** > **Kurumsal tümleştirme** > **mantıksal uygulama**.

   ![Mantıksal uygulama oluşturma](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. Aşağıdaki tablonun hello belirtilen hello ayarlarla mantıksal uygulamanızı oluşturun:

   ![Uygulama Ayrıntıları mantığı sağlar](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | Ayar | Önerilen değer | Açıklama | 
   | ------- | --------------- | ----------- | 
   | **Ad** | *{mantığı-uygulamanızın-adı}* | Bir benzersiz mantığı uygulama adı sağlayın. | 
   | **Abonelik** | *{your-Azure-} aboneliği* | Bu öğreticideki tüm hizmetler aynı Azure aboneliği seçin hello. | 
   | **Kaynak grubu** | *{your-Azure-resource-group}* | Select tüm hizmetler için aynı Azure kaynak grubu Bu öğreticide hello. | 
   | **Konum** | *{your-Azure-bölgesindeki zaman}* | Select tüm hizmetler için aynı bölgede Bu öğreticide hello. | 
   | | | 

4. Hazır olduğunuzda, seçin **PIN toodashboard**ve seçin **oluşturma**.

   Mantıksal uygulamanız için bir Azure kaynağı şimdi oluşturduğunuzu düşünün. 
   Azure mantıksal uygulamanızı dağıtıldıktan sonra hello Logic Apps Tasarımcısı, daha hızlı başlayabilirsiniz, şablonları için ortak desenler gösterir.

   > [!NOTE] 
   > Seçtiğinizde, **PIN toodashboard**, mantıksal uygulamanızı Logic Apps Tasarımcısı'nda otomatik olarak açılır. Aksi takdirde, el ile bulabilir ve mantıksal uygulamanızı açın.

5. Şimdi mantıksal uygulama şablonu seçin. Altında **şablonları**, seçin **boş mantıksal uygulama** mantıksal uygulamanızı sıfırdan oluşturabilirsiniz.

   ![Mantıksal uygulama şablonu seçin](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   Merhaba Logic Apps Tasarımcısı şimdi gösterir, [ *Bağlayıcılar* ](../connectors/apis-list.md) ve [ *Tetikleyicileri* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) , mantıksal uygulama ve ayrıca Eylemler toostart kullanabilirsiniz bir tetikleyici tooperform görevleri sonra olduğunu ekleyebilirsiniz. Bir tetikleyici bir mantıksal uygulama örneği oluşturur ve logic app akışınızı başlatan bir olaydır. 
   Mantıksal uygulamanızı bir tetikleyici hello ilk öğe olarak gerekir.

6. Merhaba arama kutusuna "olay kılavuz", filtre olarak girin. Bu tetikleyici seçin: **Azure olay Kılavuzu - kaynak olayı**

   ![Bu tetikleyici seçin: "Azure olay Kılavuzu - kaynak olay"](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. İstendiğinde, tooAzure olay kılavuz Azure kimlik bilgilerinizle oturum açın.

   ![Azure kimlik bilgilerinizle oturum](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > Kişisel bir Microsoft hesabıyla oturum gibi kapattığınızdan varsa @outlook.com veya @hotmail.com, hello olay kılavuz tetikleyici değil görüntülenebilir doğru. Geçici bir çözüm olarak seçin [Connect ile hizmet sorumlusu](/azure-resource-manager/resource-group-create-service-principal-portal.md), veya hello Azure aboneliğinizle, örneğin, ilişkili Azure Active Directory bir üyesi olarak kimlik doğrulaması *kullanıcı adı* @emailoutlook.onmicrosoft.com.

8. Şimdi mantıksal uygulama toopublisher olaylarınızı abone olun. Aşağıdaki tablonun hello belirtildiği gibi olay aboneliğinizin Hello bilgileri sağlayın:

   ![Ayrıntılar için olay abonelik sağlayın](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | Ayar | Önerilen değer | Açıklama | 
   | ------- | --------------- | ----------- | 
   | **Abonelik** | *{sanal makine-Azure-abonelik}* | Merhaba olay publisher'ın Azure aboneliğini seçin. Bu öğretici için hello sanal makineniz için Azure aboneliği seçin. | 
   | **Kaynak Türü** | Microsoft.Resources.resourceGroups | Merhaba olay publisher'ın kaynak türü seçin. Yalnızca kaynak grupları mantıksal uygulamanızı izler şekilde Bu öğretici için belirtilen değer Seç hello. | 
   | **Kaynak adı** | *{sanal-makine-resource-grup-adı}* | Merhaba publisher'ın kaynak adı seçin. Bu öğreticide, sanal makineniz için hello hello kaynak grubunun adını seçin. | 
   | İsteğe bağlı ayarlarını seçin **Gelişmiş Seçenekleri Göster**. | *{açıklamalarına bakın}* | * **Filtre önek**: Bu öğretici için bu ayarı boş bırakın. Merhaba varsayılan davranışı tüm değerleri eşleşir. Bununla birlikte, örneğin, bir yol ve belirli bir kaynak için bir parametre bir filtre olarak önek dizesi belirtebilirsiniz. <p>* **Sonek filtre**: Bu öğretici için bu ayarı boş bırakın. Merhaba varsayılan davranışı tüm değerleri eşleşir. Ancak, yalnızca belirli dosya türlerini istediğinizde bir filtre, örneğin, bir dosya adı uzantısı, sonek dizesi belirtebilirsiniz.<p>* **Abonelik adı**: olay aboneliğiniz için benzersiz bir ad sağlayın. |
   | | | 

   İşiniz bittiğinde, olay kılavuz tetikleyicisi bu örnekteki gibi görünebilir:
   
   ![Örnek olay kılavuz tetikleyici ayrıntıları](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. Mantıksal uygulamanızı kaydedin. Merhaba designer araç çubuğundan seçin **kaydetmek**. toocollapse ve Gizle mantıksal uygulamanızı ayrıntılarında bir eylemin hello eylemin başlık çubuğu seçin.

   ![Mantıksal uygulamanızı kaydetme](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   Mantıksal uygulamanızı bir olay kılavuz tetikleyicisi ile kaydettiğinizde, Azure logic app seçili tooyour kaynağınız için bir olay aboneliği otomatik olarak oluşturur. Bu nedenle Hello kaynak bir olay toohello olay kılavuz yayımlandığında, bu olay kılavuz otomatik olarak hello olay tooyour mantıksal uygulama iter. Bu olay mantıksal uygulamanızı tetikler sonra oluşturur ve sonraki adımları tanımladığınız hello iş akışı örneğini çalıştırır.

Mantıksal uygulamanız artık canlı ve tooevents hello olay kılavuz gelen dinler, ancak Eylemler toohello iş akışı ekleyene kadar hiçbir şey yapmaz. 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a>Sanal makine değişiklikleri denetleyen bir koşul Ekle

toorun yalnızca belirli bir olay gerçekleştiğinde mantığı uygulama iş akışınız için sanal makine "yazma işlemlerini" denetleyen bir koşul ekleyin. Bu koşul true olduğunda, mantıksal uygulamanızı güncelleştirilmiş hello sanal makineye ilişkin ayrıntıları içeren e-posta gönderir.

1. Mantıksal Uygulama Tasarımcısı'nda hello olay kılavuz tetikleyici altında seçin **yeni adım** > **bir koşul eklemek**.

   ![Bir koşul tooyour mantıksal uygulama Ekle](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   Merhaba mantığı Uygulama Tasarımcısı hello koşul true veya false olup tabanlı eylem yolları toofollow dahil olmak üzere bir boş koşulu tooyour iş akışı, ekler.

   ![Boş koşulu](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. Merhaba, **koşulu** kutusunda, seçin **Gelişmiş modda Düzenle**.
Bu ifade girin:

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   Koşulunuz şimdi aşağıdaki gibi görünür:

   ![Boş koşulu](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   Bu ifade hello olayı denetler `body` için bir `data` hello burada nesne `operationName` özelliktir hello `Microsoft.Compute/virtualMachines/write` işlemi. 
   Daha fazla bilgi edinmek [olay kılavuz olay şema](../event-grid/event-schema.md).

3. tooprovide hello koşul için bir açıklama seçin hello **üç nokta** (**...** ) düğmesini hello koşul şekli ve ardından **yeniden adlandırma**.

   > [!NOTE] 
   > Merhaba Bu öğreticide daha sonra örnekler de hello mantığı uygulama akışındaki adımları için açıklamalar sağlar.

4. Artık seçim **temel modunda Düzenle** böylece hello ifade gösterildiği gibi otomatik olarak çözer:

   ![Mantıksal uygulama durumu](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. Mantıksal uygulamanızı kaydedin.

## <a name="send-email-when-your-virtual-machine-changes"></a>Sanal makineniz değiştiğinde e-posta Gönder

Şimdi ekleyin bir [ *eylem* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) böylece hello koşul doğruysa belirtildiğinde, bir e-posta alırsınız.

1. Merhaba koşulunda'nın **true ise** kutusunda, seçin **Eylem Ekle**.

   ![Koşul true olduğunda için Eylem Ekle](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. Merhaba arama kutusuna "e-posta", filtre olarak girin. E-posta sağlayıcınız üzerinde bağlı olarak, bulun ve hello eşleşen Bağlayıcısı'nı seçin. Ardından, bağlayıcı için hello "e-posta Gönder" eylemini seçin. Örneğin: 

   * Azure iş veya Okul hesabı seçme hello Office 365 Outlook Bağlayıcısı. 
   * Kişisel Microsoft hesapları için hello Outlook.com bağlayıcıyı seçin. 
   * Gmail hesapları için hello Gmail bağlayıcıyı seçin. 

   Merhaba Office 365 Outlook Bağlayıcısı ile toocontinue yapacağız. 
   Farklı bir sağlayıcı kullanırsanız, adımları kalır hello hello aynı ancak UI farklı görünebilir. 

   !["E-posta Gönder" eylemini seçin](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. E-posta sağlayıcınız için bir bağlantı zaten yoksa, kimlik doğrulaması için sorulduğunda tooyour e-posta hesabı oturum açın.

4. Aşağıdaki tablonun hello belirtildiği gibi hello e-posta için bilgileri sağlayın:

   ![Boş bir e-posta eylemi](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > İş akışınızda, kullanılabilir alandan tooselect tıklatın bir düzenleme kutusuna kadar bu hello **dinamik içerik** açılır liste veya seçin **dinamik içerik eklemek**. Daha fazla alan için seçin **daha fazla** hello listesindeki her bölüm için. tooclose hello **dinamik içerik** listesinde, seçin **dinamik içerik eklemek**.

   | Ayar | Önerilen değer | Açıklama | 
   | ------- | --------------- | ----------- | 
   | **Hedef** | *{Alıcı e-posta adresi}* |Merhaba alıcının e-posta adresi girin. Test amacıyla, kendi e-posta adresini kullanabilirsiniz. | 
   | **Konu** | Güncelleştirilmiş kaynak: **konu**| Merhaba içerik hello e-postanın konusunu girin. Bu öğretici için girin hello önerilen metin ve select hello olayın **konu** alan. Burada, e-posta konusu hello adı güncelleştirilmiş hello kaynağın (sanal makine) içerir. | 
   | **Gövde** | Kaynak grubu: **konu** <p>Olay türü: **olay türü**<p>Olay Kimliği: **kimliği**<p>Süre: **olay süresi** | Merhaba içerik hello e-postanın gövdesi için girin. Bu öğretici için girin hello önerilen metin ve select hello olayın **konu**, **olay türü**, **kimliği**, ve **olay süresi** alanları böylece e-postanızı hello kaynak grubu adı, olay türü, olay zaman damgası ve hello güncelleştirmesi olay Kimliğini içerir. <p>içeriğinizi boş satırlarda tooadd SHIFT + Enter tuşuna basın. | 
   | | | 

   > [!NOTE] 
   > Merhaba Tasarımcısı otomatik olarak ekler, bir dizi temsil eden bir alan seçerseniz, bir **her** hello dizi başvuran hello eylem çevresine daire. Bu şekilde, mantıksal uygulamanızı her dizi öğesi üzerinde bu eylemi gerçekleştirir.

   Şimdi, e-posta eyleminizi aşağıdaki örnekte olduğu gibi görünebilir:

   ![E-postayla çıkışları tooinclude seçin](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   Ve tamamlanmış mantıksal uygulamanızı bu örnekteki gibi görünmelidir:

   ![Tamamlanmış mantıksal uygulama](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. Mantıksal uygulamanızı kaydedin. toocollapse ve Gizle mantıksal uygulamanızı ayrıntılarında her eylemin hello eylemin başlık çubuğu seçin.

   ![Mantıksal uygulamanızı kaydetme](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   Mantıksal uygulamanız artık canlı, ancak hiçbir şey yapmadan önce değişiklikleri tooyour sanal makine için bekler. 
   tootest mantıksal uygulamanızı toohello sonraki bölümde şimdi devam edin.

## <a name="test-your-logic-app-workflow"></a>Mantıksal uygulama akışınızı test

1. mantıksal uygulamanızı hello almaktır toocheck olayları belirtilen, sanal makinenizi güncelleştirin. 

   Örneğin, sanal makinenizde hello Azure portal boyutlandırabilirsiniz veya [Azure PowerShell ile VM'yi yeniden boyutlandırın](../virtual-machines/windows/resize-vm.md). 

   Birkaç dakika sonra bir e-posta almanız gerekir. Örneğin:

   ![Sanal makine güncelleştirmesi hakkında e-posta](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. tooreview hello çalıştırır ve logic app menünüzde mantığı uygulamanız için tetikleyici geçmişi seçin **genel bakış**. tooview bir çalıştırma hakkında daha fazla ayrıntı seçin hello satır çalıştırılan için.

   ![Mantıksal uygulama geçmişi çalıştırır](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. tooview hello girişleri ve çıkışları her adımı için tooreview istediğiniz hello adım genişletin. Bu bilgiler tanılamanıza ve sorunları mantığı uygulamanızda hata ayıklama yardımcı olabilir.
 
   ![Mantıksal uygulama geçmiş ayrıntıları çalıştırın](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

Tebrikler, oluşturduğunuz ve bir olay kılavuz aracılığıyla kaynak olaylarını izler ve olaylar oluştuğunda e-postalar bir mantıksal uygulama çalıştırın. Ayrıca, sistemleri tümleştirme süreçlerini otomatikleştirmek ve bulut Hizmetleri iş akışları ne kadar kolay oluşturabilirsiniz öğrendiniz.

## <a name="clean-up-resources"></a>Kaynakları temizleme

Bu öğretici kaynaklarını kullanır ve Azure aboneliğinize üzerinde ücretlendirme eylemleri gerçekleştirir. Hello eğitim ve test bittiğinde, bu nedenle devre dışı bırakır veya tooincur ücretleri burada istemediğiniz tüm kaynakları silmesini emin olun.

Mantıksal uygulamanızı çalıştıran ve hello uygulama silmeden e-posta gönderme durdurabilirsiniz. Mantıksal uygulama menünüzde seçin **genel bakış**. Merhaba araç çubuğunda seçin **devre dışı**.

![Mantıksal uygulamanızı devre dışı bırakma](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a>SSS

**Q**: hangi diğer sanal görevleri izleme makine olay kılavuzları ve logic apps ile yapabilir miyim? </br>
**A**: örneğin başka yapılandırma değişiklikleri izleyebilirsiniz:

* Bir sanal makine rol tabanlı erişim denetimi (RBAC) hakları alır.
* Bir ağ arabiriminde (NIC) tooa ağ güvenlik grubu (NSG) yapılan değişiklikler.
* Sanal makinesi için diskler eklenir veya kaldırılır.
* Bir ortak IP adresi tooa sanal makine NIC atanır

## <a name="next-steps"></a>Sonraki adımlar

* [Olay kılavuz genel bakış](../event-grid/overview.md)
* [Olay kılavuz kavramları](../event-grid/concepts.md)
* [Hızlı Başlangıç: Oluşturmak ve olay kılavuz özel olaylarla rota](../event-grid/custom-event-quickstart.md)
* [Kılavuz olay şeması](../event-grid/event-schema.md)
* [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)
* [Önceden tanımlanmış şablonları ile uygulama iş mantığı oluşturun](../logic-apps/logic-apps-use-logic-app-templates.md)