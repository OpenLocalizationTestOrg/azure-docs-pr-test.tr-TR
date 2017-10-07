---
title: "aaaGet özel şablonlarla çalışmaya | Microsoft Docs"
description: "Ekleme, yönetme ve hello Azure portal, hello Azure CLI veya PowerShell kullanarak özel şablonlarınızı paylaşma."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a>Hello Azure Portal'da özel şablonları kullanmaya başlama
Bir [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) şablonudur bildirim temelli bir şablondur dağıtımınızı toodefine kullanılır. Merhaba kaynakları toodeploy bir çözüm için tanımlayın ve parametreleri ve farklı ortamlar için tooinput değerleri etkinleştir değişkenleri belirtin. Merhaba şablon JSON ve kullanabileceğiniz ifadeler oluşur dağıtımınız için tooconstruct değerleri.

Merhaba yeni kullanabilirsiniz **şablonları** hello özelliği [Azure Portal](https://portal.azure.com) hello birlikte **Microsoft.Gallery** bir uzantısı olarak hello kaynak sağlayıcısı [ Azure Market](https://azure.microsoft.com/marketplace/) tooenable kullanıcılar toocreate, yönetmek ve kişisel bir kitaplıktan özel şablonları dağıtabilirsiniz.

Bu belge, ekleme, yönetme ve özel paylaşım yoluyla anlatan **şablonu** hello Azure Portal kullanarak.

## <a name="guidance"></a>Rehber
Merhaba aşağıdaki önerileri tam anlamıyla yararlanabilmek yardımcı olacak **şablonları** çözümleriniz üzerinde çalışırken:

* Bir **Şablon**, Resource Manager şablonu ve ek meta verileri içeren kapsayıcı bir kaynaktır. Merhaba Market tooan öğesinde çok benzer şekilde davranır. Hello önemli fark, özel bir öğe genel Market öğelerinin karşılıklı toohello olmasıdır.
* Merhaba **şablonları** kitaplığı, dağıtımlarını iyi toocustomize isteyen kullanıcılar için çalışır.
* **Şablonlar**, Azure içinde basit bir depoya ihtiyaç duyan kullanıcılar için iyi çalışır.
* Var olan bir Resource Manager şablonu ile başlayın. [GitHub](https://github.com/Azure/azure-quickstart-templates)'da şablon bulun veya var olan bir kaynak grubundan [Şablonu dışarı aktarın](../azure-resource-manager/resource-manager-export-template.md).
* **Şablonları** , kendilerini yayımlayan bağlı toohello kullanıcı. okuma erişimi tooit sahip görünür tooeveryone Hello yayımcı adıdır.
* **Şablonlar**, Resource Manager kaynaklarıdır ve yayımlandıktan sonra yeniden adlandırılamaz.

## <a name="add-a-template-resource"></a>Şablon kaynağı ekleme
İki yolu toocreate vardır bir **şablonu** hello Azure portal kaynak.

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a>1. Yöntem: Çalışan bir kaynak grubundan yeni bir Şablon kaynağı oluşturma
1. Hello Azure Portal tooan mevcut kaynak grubuna gidin. **Ayarlar**'da **Şablonu dışarı aktarma** öğesini seçin.
2. Merhaba Resource Manager şablonunu dışarı aktarıldıktan sonra hello kullan **Şablonu Kaydet** düğmesini toosave, toohello **şablonları** deposu. Şablonu dışarı aktarmayla ilgili tüm ayrıntıları [burada](../azure-resource-manager/resource-manager-export-template.md) bulabilirsiniz.
   <br /><br />
   ![Kaynak grubunu dışarı aktarma](media/rg-export-portal1.PNG)  <br />
3. Select hello **tooTemplate kaydetmek** komut düğmesi.
   <br /><br />
4. Aşağıdaki bilgilerle hello girin:
   
   * Adı – hello şablon nesnesinin adı (Not: Bu Azure Resource Manager temelli adıdır. Tüm adlandırma kısıtlamaları geçerlidir ve oluşturulduktan sonra değiştirilemez).
   * Açıklama – hello şablonla ilgili kısa bir Özet.
     
     ![Şablonu kaydetme](media/save-template-portal1.PNG)  <br />
5. **Kaydet** düğmesine tıklayın.
   
   > [!NOTE]
   > Merhaba dışarı aktarma şablonu dikey bildirimleri hello dışarı aktarılan Resource Manager şablonu hata var, ancak mümkün toosave olmaya devam eder Bu Resource Manager şablonu toohello şablonları gösterir. Denetleyin ve yeniden dağıtırken hello Resource Manager şablonunu dışarı önce tüm Resource Manager şablonu sorunlarını düzeltmek emin olun.
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a>2. Yöntem: Gözat bölümünden yeni bir Şablon kaynağı ekleme
Ayrıca, yeni bir ekleyebilirsiniz **şablonu** hello + Ekle komut düğmesini kullanarak sıfırdan **Gözat > şablonlar**. Bir ad, açıklama ve Resource Manager şablonu JSON hello tooprovide gerekir.

![Şablon ekleme](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> Microsoft.Gallery, Kiracı bazlı bir Azure kaynak sağlayıcısıdır. Merhaba şablon kaynağı oluşturulduğu bağlı toohello kullanıcıdır. Bu bağlı tooany belirli aboneliği değil. Bir abonelik yalnızca bir şablon dağıtılırken seçilen toobe gerekir.
> 
> 

## <a name="view-template-resources"></a>Şablon kaynaklarını görüntüleme
Tüm **şablonları** kullanılabilir tooyou adresindeki görülme **Gözat > şablonlar**. Buna, oluşturduğunuz **Şablonlar**'ın yanı sıra, farklı izin düzeyleriyle sizinle paylaşılanlar da dahildir. Merhaba, daha fazla ayrıntı [erişim denetimi](#access-control-for-a-tenant-resource-provider) bölümüne bakın.

![Şablonu görüntüleme](media/view-template-portal1.PNG)  <br />

Merhaba ayrıntılarını görüntüleyebilirsiniz bir **şablonu** hello listedeki bir öğeye tıklayarak.

![Şablonu görüntüleme](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a>Şablon kaynağını düzenleme
Hello için düzenleme akışını başlatabilirsiniz bir **şablonu** hello öğede sağ tıklayarak hello Gözat listesi veya hello Düzenle komutu düğmesini seçerek.

![Şablon düzenleme](media/edit-template-portal1a.PNG)  <br />

Merhaba açıklamayı veya Resource Manager şablonu metnini düzenleyebilirsiniz. Bir Resource Manager kaynak adı olduğundan hello adını düzenleyemezsiniz. Merhaba Resource Manager şablonu JSON düzenlediğinizde biz tooensure geçerli JSON olduğunu doğrular. Seçin **Tamam** ve ardından **kaydetmek** toosave güncelleştirilmiş şablonunuzu.

![Şablon düzenleme](media/edit-template-portal2a.PNG)  <br />

Bir kez hello **şablonu** kaydedilen bir onay bildirimi görürsünüz.

![Şablon düzenleme](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a>Bir Şablon kaynağını dağıtma
**Okuma** izniniz olan herhangi bir **Şablon**'u dağıtabilirsiniz. Merhaba dağıtım akışı hello standart Azure şablon dağıtımı dikey penceresini başlatır. Merhaba Resource Manager şablonu parametreleri tooproceed hello dağıtımı ile Merhaba değerlerini doldurun.

![Şablon dağıtma](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a>Şablon kaynağı paylaşma
Bir **Şablon** kaynağı iş arkadaşlarınızla paylaşılabilir. Paylaşımı davranır benzer şekilde çok[Azure ile ilgili herhangi bir kaynak için rol ataması](../active-directory/role-based-access-control-configure.md). Merhaba **şablonu** sahip bir şablon kaynağıyla etkileşim kurabilen tooother kullanıcılara izinler sağlar. Merhaba kişi veya grup hello paylaştığınız kişilerin **şablonu** mümkün toosee hello Resource Manager şablonunu ve bunun galeri özelliklerini ile sonuna olacaktır.

### <a name="access-control-for-hello-microsoftgallery-resources"></a>Merhaba Microsoft.Gallery kaynakları için erişim denetimi
| Rol | İzinler |
| --- | --- |
| Sahip |Merhaba şablon kaynağı paylaşma dahil olmak üzere üzerinde tam denetim verir |
| Okuyucu |Şablon kaynağı hello üzerinde okuma ve Execute(Deploy) verir |
| Katılımcı |Şablon kaynağı hello üzerinde düzenleme ve silme izni verir. Kullanıcı hello şablon başkalarıyla paylaşamaz |

Seçin **paylaşımı** hello Gözat öğesine sağ tıklayarak veya belirli bir öğenin hello görünümü dikey. Bu, bir Paylaşma deneyimini çalıştırır.

![Şablonu paylaşma](media/share-template-portal1a.png)  <br />

 Bir rolü ve bir kullanıcı veya grup tooprovide erişim tooa belirli artık seçebilirsiniz **şablon**. Merhaba kullanılabilir roller sahip, okuyucu ve katkıda bulunan ' dir. Merhaba, daha fazla ayrıntı [erişim denetimi](#access-control-for-a-tenant-resource-provider) yukarıdaki bölümde.

![Şablonu paylaşma](media/share-template-portal2b.png)  <br />

![Şablonu paylaşma](media/share-template-portal3b.png)  <br />

**Seç**'e ve **Tamam**'a tıklayın. Şimdi hello kullanıcıları veya grupları görebilirsiniz toohello kaynak eklendi.

![Şablonu paylaşma](media/share-template-portal4b.png)  <br />

> [!NOTE]
> Bir şablonu yalnızca kullanıcılar ve gruplar ile hello paylaşılabilir aynı Azure Active Directory kiracısı. Kiracınızda olmayan e-posta adresi olan bir şablonu paylaşıyorsanız, hello kullanıcı toojoin hello Kiracı konuk olarak soran bir davet gönderilir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Resource Manager şablonları oluşturma hakkında daha fazla toolearn bakın [şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)
* bir Resource Manager şablonunda kullanabileceğiniz toounderstand hello işlevleri bkz [şablon işlevleri](../azure-resource-manager/resource-group-template-functions.md)
* Şablonlarınızı tasarlama konusunda rehberlik için bkz. [Azure Resource Manager şablonları oluşturmaya yönelik en iyi uygulamalar](../azure-resource-manager/best-practices-resource-manager-design-templates.md)

