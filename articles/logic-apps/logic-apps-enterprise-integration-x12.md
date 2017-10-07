---
title: "B2B Kurumsal tümleştirme - Azure Logic Apps için aaaX12 iletileri | Microsoft Docs"
description: "Azure Logic Apps ile B2B Kurumsal tümleştirme EDI biçimindeki Exchange X12 iletiler"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 20a077b299875a16ada66a500d5f1c8f9972d309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a>Logic apps ile Kurumsal tümleştirme için Exchange X12 iletileri

X12 exchange önce iletileri Azure mantıksal uygulamaları için bir X12 oluşturmalısınız sözleşmesi ve bu anlaşma tümleştirme hesabınızı depolamak. Merhaba adımlar şunlardır toocreate X12 bir anlaşma.

> [!NOTE]
> Bu sayfa, Azure mantıksal uygulamaları için hello X12 özelliklerini kapsar. Daha fazla bilgi için bkz: [EDIFACT](logic-apps-enterprise-integration-edifact.md).

## <a name="before-you-start"></a>Başlamadan önce

Gereksinim duyduğunuz hello öğeleri şöyledir:

* Bir [tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-accounts.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili
* En az iki [ortakları](../logic-apps/logic-apps-enterprise-integration-partners.md) , tümleştirme hesabınızda tanımlanır ve altında hello X12 tanımlayıcıyla yapılandırılmış **iş kimlikleri**    
* Gerekli [şema](../logic-apps/logic-apps-enterprise-integration-schemas.md) tooyour yüklemeyle [tümleştirme hesabı](../logic-apps/logic-apps-enterprise-integration-accounts.md)

Çalıştırdıktan sonra [tümleştirme hesap oluşturmak](../logic-apps/logic-apps-enterprise-integration-accounts.md), [ortakları eklemek](logic-apps-enterprise-integration-partners.md)ve bir [şema](../logic-apps/logic-apps-enterprise-integration-schemas.md) toouse istediğiniz, bir X12 oluşturabileceğiniz aşağıdaki adımları izleyerek anlaşma.

## <a name="create-an-x12-agreement"></a>Bir X12 oluşturma Sözleşmesi

1.  İçinde toohello oturum [Azure portal](http://portal.azure.com "Azure portal"). Merhaba sol menüden seçin **daha fazla hizmet**. 

    > [!TIP]
    > Görmüyorsanız, **daha fazla hizmet**, tooexpand hello menü ilk olabilir. Daraltılmış hello menü Hello üstünde seçin **Göster menüsü**.

    ![Sol menüsünde "Daha fazla Hizmetleri" öğesini seçin](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  Merhaba arama kutusuna "tümleştirme", filtre olarak yazın. Merhaba sonuçları listesinden seçmek **tümleştirme hesapları**.  

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. Merhaba, **tümleştirme hesapları** açılır ve select hello tümleştirme hesabını tooadd hello sözleşmesi istediğiniz dikey.
Herhangi bir tümleştirme hesabı görmüyorsanız, [oluşturmak ilk](../logic-apps/logic-apps-enterprise-integration-accounts.md "tümleştirme hesapları hakkında").

    ![Burada toocreate hello sözleşmesi tümleştirme hesabı seçin](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. Seçin **genel bakış**seçeneğini belirleyip hello **anlaşmaları** döşeme. Anlaşmaları döşeme yoksa, ilk hello kutucuğu ekleyin. 

    !["Anlaşmaları" kutucuğunu seçin](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Açılan hello anlaşmaları dikey penceresinde, seçin **Ekle**.

    !["Ekle" yi seçin](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. Altında **Ekle**, girin bir **adı** sözleşmenizi için. Merhaba anlaşma türünü seçin **X12**. Select hello **ana iş ortağı**, **konak kimliği**, **Konuk iş ortağı**, ve **Konuk kimlik** sözleşmenizi için. Daha fazla özellik Ayrıntılar için bu adımda hello tabloya bakın.

    ![Anlaşma ayrıntılarını sağlayın](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | Özellik | Açıklama |
    | --- | --- |
    | Ad |Merhaba anlaşma adı |
    | Anlaşma türü | X12 olmalıdır |
    | Ana bilgisayar iş ortağı |Bir anlaşma hem konak hem de Konuk iş ortağı gerekir. Merhaba konak ortağı hello sözleşmesi yapılandırır hello kuruluşu temsil eder. |
    | Ana bilgisayar kimliği |Merhaba ana iş ortağı için bir tanımlayıcı |
    | Konuk iş ortağı |Bir anlaşma hem konak hem de Konuk iş ortağı gerekir. Merhaba Konuk ortağı hello konak ortak iş yapmakta hello kuruluşu temsil eder. |
    | Konuk kimlik |Merhaba Konuk iş ortağı için bir tanımlayıcı |
    | Ayarlarını alma |Bu özellikleri anlaşmanın tarafından alınan tooall iletileri geçerlidir. |
    | Gönderme ayarları |Bu özellikleri anlaşmanın tarafından gönderilen tooall iletileri geçerlidir. |  

  > [!NOTE]
  > Merhaba gönderen Niteleyici Tanımlayıcısı ve hello alıcı niteleyicisi ve hello iş ortakları ve gelen ileti içinde tanımlanan bir tanımlayıcı eşleşen anlaşma bağlıdır X12 çözünürlüğü. Bu değerler için ortağınız değiştirirseniz, hello sözleşmesi çok güncelleştirin.

## <a name="configure-how-your-agreement-handles-received-messages"></a>Anlaşma tanıtıcıları iletileri nasıl alınan yapılandırma

Merhaba sözleşmesi özelliklerini ayarladıysanız, bu anlaşmanın nasıl tanımlar ve bu anlaşma ile ortaktan alınan gelen iletileri işleme yapılandırabilirsiniz.

1.  Altında **Ekle**seçin **alma ayarı**.
Bu özellikleri sözleşmenizi iletiler birlikte alış verişleri hello ortağıyla göre yapılandırın. Özellik açıklamaları için bu bölümdeki hello tablolara bakın.

    **Alma ayarlarını** şu bölümlere düzenlenmiştir: tanımlayıcılar, bildirim, şemaları, zarflar, denetim numaraları, doğrulama ve iç ayarlar.

2. Bitirdikten sonra emin toosave ayarlarınızı seçerek olun **Tamam**.

Şimdi sözleşmenizi hazır toohandle gelen ayarları seçili tooyour uygun iletileri.

### <a name="identifiers"></a>Tanımlayıcıları

![Tanımlayıcı özelliklerini ayarlama](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| Özellik | Açıklama |
| --- | --- |
| ISA1 (yetkilendirme niteleyici) |Merhaba yetkilendirme niteleyici değeri hello aşağı açılan listeden seçin. |
| ISA2 |İsteğe bağlı. Yetkilendirme bilgileri değeri girin. Merhaba değer ISA1 için girdiğiniz dışında 00 ise, en az bir alfasayısal karakter ve en fazla 10 girin. |
| ISA3 (Güvenlik niteleyicisi) |Merhaba Güvenlik niteleyicisi değeri hello aşağı açılan listeden seçin. |
| ISA4 |İsteğe bağlı. Merhaba güvenlik bilgileri değeri girin. Merhaba değer ISA3 için girdiğiniz dışında 00 ise, en az bir alfasayısal karakter ve en fazla 10 girin. |

### <a name="acknowledgment"></a>Bildirim

![Bildirim özelliklerini ayarlama](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| Özellik | Açıklama |
| --- | --- |
| Beklenen TA1 |Teknik Bildirim toohello değişim gönderen döndürür |
| Beklenen FA |İşlev bildirim toohello değişim gönderen döndürür. Merhaba 997 veya 999 bildirimler istediğinizi seçin hello şema sürümünde temel |
| AK2/IK2 döngü içerir |Kabul edilen işlem kümeleri için işlevsel bildirimler AK2 döngüler nesil sağlar |

### <a name="schemas"></a>Şemalar

Her işlem türü (ST1) ve gönderen uygulama (GS2) için bir şema seçin. Merhaba alma ardışık düzeni için ST1 hello değerleri eşleştirerek hello gelen ileti ayrıştırır ve iletide hello gelen hello GS2 değerleri,, Grup İlkesi ve burada ayarladığınız hello şemasıyla hello şema hello gelen ileti.

![Şema seçin](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| Özellik | Açıklama |
| --- | --- |
| Sürüm |Merhaba X12 sürümü seçin |
| İşlem türü (ST01) |Merhaba hareket türü seçin |
| Gönderen uygulama (GS02) |Merhaba gönderen uygulama seçin |
| Şema |Toouse istediğiniz hello şema dosyasını seçin. Şemalar tooyour tümleştirme hesabı eklenir. |

> [!NOTE]
> Gerekli hello yapılandırma [şema](../logic-apps/logic-apps-enterprise-integration-schemas.md) diğer bir deyişle karşıya yüklenen tooyour [tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Zarflar

![Bir işlem kümesinde Hello ayırıcı belirtin: Standart tanımlayıcı veya yineleme ayırıcı seçin](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| Özellik | Açıklama |
| --- | --- |
| ISA11 kullanımı |Merhaba ayırıcı toouse bir işlem kümesinde belirtir: <p>Seçin **standart tanımlayıcı** toouse bir nokta (.) hello gelen hello EDI belgede ondalık gösterimindeki hello yerine ondalık gösterimde için ardışık düzen alırsınız. <p>Seçin **yineleme ayırıcı** toospecify hello ayırıcı yinelenen yinelemelerini basit veri öğesi veya yinelenen veri yapısı. Örneğin, genellikle hello ayar (^) hello yineleme ayırıcı olarak kullanılır. HIPAA şemalarda hello ayar yalnızca kullanabilirsiniz. |

### <a name="control-numbers"></a>Denetim numaraları

![Nasıl toohandle kontrol sayı çoğaltmaları seçin](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| Özellik | Açıklama |
| --- | --- |
| Değişim kontrol numarası çoğaltmaları izin verme |Yinelenen etkileşimler engelleyin. Alınan hello Değişim Denetimi numarasını Hello Değişim Denetimi numarası (ISA13) denetler. Bir eşleşme algılanırsa, hello alma ardışık düzen hello değişim işlem değil. Hello için bir değer vererek hello denetimi gerçekleştirmek için gün sayısını belirtebilirsiniz *denetlemek için yinelenen ISA13 her (gün)*. |
| Yinelenen Grup denetim numaralarına izin verme |Blok yinelenen grup denetimi numaralarıyla interchanges. |
| Yinelenen İşlem kümesi denetim numaralarına izin verme |Blok yinelenen işlem kümesi denetim numaralarıyla interchanges. |

### <a name="validations"></a>Doğrulama

![Alınan iletilerin doğrulama özelliklerini ayarlama](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

Her doğrulama satır tamamladığınızda, başka bir otomatik olarak eklenir. Herhangi bir kuralın belirtmezseniz, doğrulama hello "Varsayılan" satır kullanır.

| Özellik | Açıklama |
| --- | --- |
| İleti türü |Merhaba EDI ileti türünü seçin. |
| EDI doğrulama |EDI doğrulama hello şema EDI özellikleri, uzunluk kısıtlamaları, boş veri öğeleri ve sondaki ayırıcılar tarafından tanımlanan veri türleri gerçekleştirin. |
| Genişletilmiş Doğrulama |Merhaba veri türü değilse EDI, doğrulama üzerinde hello veri öğesi gereksinimdir ve yineleme, numaralandırmalar ve veri öğesi uzunluğu doğrulama (min/max) izin verilir. |
| Başında ve sonunda sıfır izin ver |Başında veya sonunda sıfır ek korumak ve karakterleri boşluk. Bu karakterleri kaldırmayın. |
| Başında ve sonunda sıfır kırpma |Baştaki veya sondaki sıfır ve boşluk karakterlerini Kaldır. |
| Sondaki ayırıcı İlkesi |Sondaki ayırıcılar oluşturur. <p>Seçin **izin** tooprohibit sonundaki sınırlayıcılar ve ayırıcı hello olarak alınan değişim. Merhaba değişim sonundaki sınırlayıcılar ve ayırıcılar varsa, hello değişim geçerli bildirilmedi. <p>Seçin **isteğe bağlı** tooaccept interchanges ile veya olmadan sonundaki sınırlayıcılar ve ayırıcılar. <p>Seçin **zorunlu** zaman hello değişim olmalıdır sonundaki sınırlayıcılar ve ayırıcılar. |

### <a name="internal-settings"></a>İç ayarları

![İç ayarlarını seçin](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| Özellik | Açıklama |
| --- | --- |
| Kapsanan ondalık biçiminde "Nn" tooa temel 10 sayısal değer Dönüştür |10 tabanında sayısal bir değer "Nn" biçiminde hello ile belirtilen bir EDI sayıyı dönüştürür |
| Sondaki ayırıcılara izin veriliyorsa boş XML etiketleri oluştur |Bu onay kutusunu toohave hello değişim gönderen dahil seçin ayırıcılar sondaki için XML etiketleri boş. |
| Değişimi işlem kümeleri olarak böl; hata durumunda işlem kümelerini askıya al|Merhaba uygun Zarf toohello işlem kümesi uygulayarak ayrı bir XML belge içine bir değişim kümesindeki her bir işlem ayrıştırır. Yalnızca hello hareketleri burada hello doğrulama başarısız askıya alır. |
| Değişimi işlem kümeleri olarak böl; hata durumunda değişimi askıya al|Merhaba uygun Zarf uygulayarak ayrı bir XML belge içine bir değişim kümesindeki her bir işlem ayrıştırır. Merhaba değişim bir veya daha fazla işlem kümelerinde doğrulama başarısız olduğunda tüm değişim askıya alır. | 
| Değişim korumak - işlem kümeleri askıya alma hatası |Merhaba değişim dokunmaz, hello tüm toplu değişim için bir XML belgesi oluşturur. Doğrulanamayan tooprocess devam ederken, hello işlem kümeleri askıya diğer tüm işlem kümeleri. |
| Değişimi koru; hata durumunda değişimi askıya al |Merhaba değişim dokunmaz, hello tüm toplu değişim için bir XML belgesi oluşturur. Merhaba değişim bir veya daha fazla işlem kümelerinde doğrulama başarısız olduğunda hello tüm değişim askıya alır. |

## <a name="configure-how-your-agreement-sends-messages"></a>Nasıl sözleşmenizi iletileri gönderir yapılandırın

Bu anlaşma nasıl tanımlar ve bu anlaşma ile tooyour ortak gönderdiğiniz giden iletilerini işleme yapılandırabilirsiniz.

1.  Altında **Ekle**seçin **gönderme ayarları**.
İletileri ile alış verişleri ortağınızla birlikte sözleşmenize göre bu özelliklerini yapılandırın. Özellik açıklamaları için bu bölümdeki hello tablolara bakın.

    **Gönderme ayarları** şu bölümlere düzenlenmiştir: tanımlayıcılar, bildirim, şemalar, zarflar, karakter kümeleri ve ayırıcılar, denetim numaraları ve doğrulama.

2. Bitirdikten sonra emin toosave ayarlarınızı seçerek olun **Tamam**.

Seçili tooyour ayarları uygun iletileri Giden hazır toohandle sözleşmenizi sunulmuştur.

### <a name="identifiers"></a>Tanımlayıcıları

![Tanımlayıcı özelliklerini ayarlama](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| Özellik | Açıklama |
| --- | --- |
| Yetkilendirme niteleyicisi (ISA1) |Merhaba yetkilendirme niteleyici değeri hello aşağı açılan listeden seçin. |
| ISA2 |Yetkilendirme bilgileri değeri girin. Bu değer dışında 00 ise, en az bir alfasayısal karakter ve en fazla 10 girin. |
| Güvenlik niteleyicisi (ISA3) |Merhaba Güvenlik niteleyicisi değeri hello aşağı açılan listeden seçin. |
| ISA4 |Merhaba güvenlik bilgileri değeri girin. Bu değer hello değeri (ISA4) metin kutusu, 00 dışında ise bir alfasayısal değer en az ve en fazla 10 girin. |

### <a name="acknowledgment"></a>Bildirim

![Bildirim özelliklerini ayarlama](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Özellik | Açıklama |
| --- | --- |
| Beklenen TA1 |Teknik Bildirim (TA1) toohello değişim gönderen döndür. Bu ayar kimin hello ileti isteklerinin hello sözleşmesi hello Konuk ortaktan bir bildirim gönderme bu hello ana iş ortağı belirtir. Bu bildirimler hello alma ayarlarına göre hello anlaşmasının hello konak ortağı tarafından beklenir. |
| Beklenen FA |İşlev bildirim (FA) toohello değişim gönderen döndür. Birlikte çalıştığınız hello şema sürümlerine göre hello 997 veya 999 onayları isteyip istemediğinizi seçin. Bu bildirimler hello alma ayarlarına göre hello anlaşmasının hello konak ortağı tarafından beklenir. |
| FA sürümü |Merhaba FA sürümü seçin |

### <a name="schemas"></a>Şemalar

![Şema toouse seçin](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Özellik | Açıklama |
| --- | --- |
| Sürüm |Merhaba X12 sürümü seçin |
| İşlem türü (ST01) |Merhaba hareket türü seçin |
| ŞEMA |Merhaba şema toouse seçin. Şemalar tümleştirme hesabınızda bulunur. Şema ilk seçerseniz, otomatik olarak sürüm ve işlem yapılandırır türü  |

> [!NOTE]
> Gerekli hello yapılandırma [şema](../logic-apps/logic-apps-enterprise-integration-schemas.md) diğer bir deyişle karşıya yüklenen tooyour [tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Zarflar

![Bir işlem kümesinde Hello ayırıcı belirtin: Standart tanımlayıcı veya yineleme ayırıcı seçin](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| Özellik | Açıklama |
| --- | --- |
| ISA11 kullanımı |Merhaba ayırıcı toouse bir işlem kümesinde belirtir: <p>Seçin **standart tanımlayıcı** toouse bir nokta (.) hello gelen hello EDI belgede ondalık gösterimindeki hello yerine ondalık gösterimde için ardışık düzen alırsınız. <p>Seçin **yineleme ayırıcı** toospecify hello ayırıcı yinelenen yinelemelerini basit veri öğesi veya yinelenen veri yapısı. Örneğin, genellikle hello ayar (^) hello yineleme ayırıcı olarak kullanılır. HIPAA şemalarda hello ayar yalnızca kullanabilirsiniz. |

### <a name="control-numbers"></a>Denetim numaraları

![Denetim numarası özelliklerini belirtin](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| Özellik | Açıklama |
| --- | --- |
| Denetim sürüm numarası (ISA12) |Merhaba X12 standart Hello sürümünü seçin |
| Kullanım göstergesi (ISA15) |Bir değişim Merhaba içeriğine seçin.  Merhaba değerler bilgi, üretim verileri veya test verileri |
| Şema |Merhaba GS ve ST kesimleri toohello ardışık düzen Gönder gönderen bir X12 kodlu değişimi için oluşturur |
| GS1 |İsteğe bağlı, hello aşağı açılan listeden hello işlevsel kod için bir değer seçin |
| GS2 |İsteğe bağlı, uygulama gönderen |
| GS3 |İsteğe bağlı, uygulama alıcı |
| GS4 |İsteğe bağlı, select CCYYMMDD ya da YYAAGG |
| GS5 |İsteğe bağlı, select SSDD, SSDDSS veya HHMMSSdd |
| GS7 |İsteğe bağlı, hello aşağı açılan listeden hello sorumlu aracısı için bir değer seçin |
| GS8 |İsteğe bağlı, hello belgenin sürümü |
| Değiş tokuş denetim numarası (ISA13) |Gerekli değerleri aralığı hello Değişim Denetimi numarasını girin. En az 1 ve en fazla 999999999 olan sayısal bir değer girin |
| Grup denetim numarası (GS06) |Gerekli bir dizi numarası hello Grup denetim numarası girin. En az 1 ve en fazla 999999999 olan sayısal bir değer girin |
| İşlem kümesi denetim numarasını (ST02) |Gerekli bir dizi numarası Merhaba işlem kümesi denetim numarasını girin. Sayısal değerleri en az 1 ve en fazla 999999999 olan bir aralığı girin |
| Alan kodu |İsteğe bağlı, bildirim içinde kullanılan işlem kümesi denetim numaraları hello aralığı için belirlenmiş. (İsteniyorsa) için hello önek ve sonek alanlara hello Orta iki alanlar için sayısal bir değer ve alfasayısal bir değer girin. Merhaba Orta alanları gereklidir ve hello ve en düşük değerler hello denetim sayısını içerir |
| Son eki |İsteğe bağlı, bir bildirim kullanılan işlem kümesi denetim numaraları hello aralığı için belirlenmiş. (İsteniyorsa) için hello önek ve sonek alanlara hello Orta iki alanlar için sayısal bir değer ve alfasayısal bir değer girin. Merhaba Orta alanları gereklidir ve hello ve en düşük değerler hello denetim sayısını içerir |

### <a name="character-sets-and-separators"></a>Karakter Kümeleri ve Ayırıcılar

Merhaba karakter kümesi dışında her ileti türü için farklı bir sınırlayıcı kümesini girebilirsiniz. Karakter kümesi için belirli bir ileti şeması belirtilmezse, hello varsayılan karakter kümesini kullanılır.

![İleti türleri için sınırlayıcılar belirtin](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| Özellik | Açıklama |
| --- | --- |
| Kullanılan karakter kümesi toobe |toovalidate hello özellikleri, select hello X12 karakter kümesi. Merhaba temel, genişletilmiş ve UTF8 seçenekleridir. |
| Şema |Bir şema hello aşağı açılan listeden seçin. Her satır tamamladıktan sonra yeni bir satır otomatik olarak eklenir. Merhaba seçili şeması ayırıcı açıklamaları aşağıdaki hello üzerinde temel toouse istediğiniz select hello ayırıcılar ayarlayın. |
| Giriş türü |Bir input type hello aşağı açılan listeden seçin. |
| Bileşen ayırıcı |tooseparate bileşik veri öğeleri, tek bir karakter girin. |
| Veri öğesi ayırıcı |bileşik veri öğeleri içindeki tooseparate basit veri öğelerinin tek bir karakter girin. |
| Değiştirme karakteri |Merhaba giden X12 iletisi oluşturulurken hello yük verilerinin tüm ayırıcı karakter değiştirmek için kullanılan bir yedek karakter girin. |
| Segment Sonlandırıcı |tooindicate hello bir EDI segmentinin sonunu tek bir karakter girin. |
| Son eki |Merhaba segment tanımlayıcı ile kullanılan hello karakteri seçin. Bir son eki atayın ve yeniden hello segment Sonlandırıcı veri öğesi boş olabilir. Merhaba segment sonlandırıcı boş bırakılırsa, sonek atamanız gerekir. |

> [!TIP]
> tooprovide özel karakter değerleri JSON olarak hello sözleşmesini düzenlemenize ve için özel karakter hello hello ASCII değeri sağlayın.

### <a name="validation"></a>Doğrulama

![İleti göndermek için doğrulama özelliklerini ayarlama](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

Her doğrulama satır tamamladığınızda, başka bir otomatik olarak eklenir. Herhangi bir kuralın belirtmezseniz, doğrulama hello "Varsayılan" satır kullanır.

| Özellik | Açıklama |
| --- | --- |
| İleti türü |Merhaba EDI ileti türünü seçin. |
| EDI doğrulama |EDI doğrulama hello şema EDI özellikleri, uzunluk kısıtlamaları, boş veri öğeleri ve sondaki ayırıcılar tarafından tanımlanan veri türleri gerçekleştirin. |
| Genişletilmiş Doğrulama |Merhaba veri türü değilse EDI, doğrulama üzerinde hello veri öğesi gereksinimdir ve yineleme, numaralandırmalar ve veri öğesi uzunluğu doğrulama (min/max) izin verilir. |
| Başında ve sonunda sıfır izin ver |Başında veya sonunda sıfır ek korumak ve karakterleri boşluk. Bu karakterleri kaldırmayın. |
| Başında ve sonunda sıfır kırpma |Baştaki veya sondaki sıfır karakterleri kaldırın. |
| Sondaki ayırıcı İlkesi |Sondaki ayırıcılar oluşturur. <p>Seçin **izin** tooprohibit sonundaki sınırlayıcılar ve ayırıcı hello olarak gönderilen değişim. Merhaba değişim sonundaki sınırlayıcılar ve ayırıcılar varsa, hello değişim geçerli bildirilmedi. <p>Seçin **isteğe bağlı** toosend interchanges ile veya olmadan sonundaki sınırlayıcılar ve ayırıcılar. <p>Seçin **zorunlu** gönderilen hello değişim sonundaki sınırlayıcılar ve ayırıcıları kullanmanız gerekiyorsa. |

## <a name="find-your-created-agreement"></a>Oluşturulan sözleşmenizi Bul

1.  Merhaba üzerinde anlaşma özelliklerinizi ayarlama işlemini tamamladıktan sonra **Ekle** dikey penceresinde, seçin **Tamam** toofinish sözleşmesi ve dönüş tooyour tümleştirme hesabı dikey oluşturma.

    Yeni eklenen sözleşmenizi artık görünür, **anlaşmaları** listesi.

2.  Ayrıca, tümleştirme hesabına genel bakış sözleşmelerinizi görüntüleyebilirsiniz. Tümleştirme hesabı dikey penceresinde, seçin **genel bakış**seçeneğini belirleyip hello **anlaşmaları** döşeme.

    ![Tüm Anlaşmalar "Anlaşmaları" döşeme tooview seçin](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-hello-swagger"></a>Görünüm hello swagger
Merhaba bkz [ayrıntıları swagger](/connectors/x12/). 

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")  

