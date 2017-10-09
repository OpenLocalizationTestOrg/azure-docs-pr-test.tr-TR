---
title: "B2B Kurumsal tümleştirme - Azure Logic Apps için aaaEDIFACT iletileri | Microsoft Docs"
description: "Azure Logic Apps ile B2B Kurumsal tümleştirme EDI biçimindeki Exchange EDIFACT iletiler"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 2257d2c8-1929-4390-b22c-f96ca8b291bc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/26/2016
ms.author: LADocs; jonfan
ms.openlocfilehash: 496fadcda58de2d36459202b839b0a63c9e5857c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-edifact-messages-for-enterprise-integration-with-logic-apps"></a>Logic apps ile Kurumsal tümleştirme için Exchange EDIFACT iletileri

Azure mantıksal uygulamaları için EDIFACT iletileri değiştirebilir önce EDIFACT sözleşmesi oluşturun ve bu anlaşma tümleştirme hesabınızı depolamak. Merhaba adımlar şunlardır toocreate EDIFACT sözleşmesi.

> [!NOTE]
> Bu sayfa, Azure mantıksal uygulamaları için hello EDIFACT özellikleri kapsar. Daha fazla bilgi için bkz: [X12](logic-apps-enterprise-integration-x12.md).

## <a name="before-you-start"></a>Başlamadan önce

Gereksinim duyduğunuz hello öğeleri şöyledir:

* Bir [tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-accounts.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili  
* En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış

> [!NOTE]
> Bir anlaşma, hello içerik almak veya tooand hello ortaktan hello anlaşma türünü eşleşmelidir gönderebileceğiniz hello iletilerinde oluşturduğunuzda.

Çalıştırdıktan sonra [tümleştirme hesap oluşturmak](../logic-apps/logic-apps-enterprise-integration-accounts.md) ve [ortakları eklemek](logic-apps-enterprise-integration-partners.md), aşağıdaki adımları izleyerek bir EDIFACT sözleşmesi oluşturabilirsiniz.

## <a name="create-an-edifact-agreement"></a>EDIFACT sözleşmesi oluşturun 

1.  İçinde toohello oturum [Azure portal](http://portal.azure.com "Azure portal"). Merhaba sol menüden seçin **daha fazla hizmet**.

    > [!TIP]
    > Görmüyorsanız, **daha fazla hizmet**, tooexpand hello menü ilk olabilir. Daraltılmış hello menü Hello üstünde seçin **Göster menüsü**.

    ![Sol menüsünde "Daha fazla Hizmetleri" öğesini seçin](./media/logic-apps-enterprise-integration-edifact/edifact-0.png)

2. Filtreniz için "tümleştirme" Merhaba arama kutusuna yazın. Merhaba sonuçları listesinden seçmek **tümleştirme hesapları**.

    ![Filtre "tümleştirme üzerinde", "Tümleştirme hesapları" seçin](./media/logic-apps-enterprise-integration-edifact/edifact-1-3.png)

3. Merhaba, **tümleştirme hesapları** açılır ve select hello tümleştirme hesabını toocreate hello sözleşmesi istediğiniz dikey.
Herhangi bir tümleştirme hesabı görmüyorsanız, [oluşturmak ilk](../logic-apps/logic-apps-enterprise-integration-accounts.md "tümleştirme hesapları hakkında").  

    ![Burada toocreate hello sözleşmesi tümleştirme hesabı seçin](./media/logic-apps-enterprise-integration-edifact/edifact-1-4.png)

4. Merhaba seçin **anlaşmaları** döşeme. Anlaşmaları döşeme yoksa, ilk hello kutucuğu ekleyin.   

    !["Anlaşmaları" kutucuğunu seçin](./media/logic-apps-enterprise-integration-edifact/edifact-1-5.png)

5. Açılan hello anlaşmaları dikey penceresinde, seçin **Ekle**.

    !["Ekle" yi seçin](./media/logic-apps-enterprise-integration-edifact/edifact-agreement-2.png)

6. Altında **Ekle**, girin bir **adı** sözleşmenizi için. İçin **anlaşma türünü**seçin **EDIFACT**. Select hello **ana iş ortağı**, **konak kimliği**, **Konuk iş ortağı**, ve **Konuk kimlik** sözleşmenizi için.

    ![Anlaşma ayrıntılarını sağlayın](./media/logic-apps-enterprise-integration-edifact/edifact-1.png)

    | Özellik | Açıklama |
    | --- | --- |
    | Ad |Merhaba anlaşma adı |
    | Anlaşma türü | EDIFACT olmalıdır |
    | Ana bilgisayar iş ortağı |Bir anlaşma hem konak hem de Konuk iş ortağı gerekir. Merhaba konak ortağı hello sözleşmesi yapılandırır hello kuruluşu temsil eder. |
    | Ana bilgisayar kimliği |Merhaba ana iş ortağı için bir tanımlayıcı |
    | Konuk iş ortağı |Bir anlaşma hem konak hem de Konuk iş ortağı gerekir. Merhaba Konuk ortağı hello konak ortak iş yapmakta hello kuruluşu temsil eder. |
    | Konuk kimlik |Merhaba Konuk iş ortağı için bir tanımlayıcı |
    | Ayarlarını alma |Bu özellikleri anlaşmanın tarafından alınan tooall iletileri geçerlidir. |
    | Gönderme ayarları |Bu özellikleri anlaşmanın tarafından gönderilen tooall iletileri geçerlidir. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Anlaşma tanıtıcıları iletileri nasıl alınan yapılandırma

Merhaba sözleşmesi özelliklerini ayarladıysanız, bu anlaşmanın nasıl tanımlar ve bu anlaşma ile ortaktan alınan gelen iletileri işleme yapılandırabilirsiniz.

1.  Altında **Ekle**seçin **alma ayarı**.
Bu özellikleri sözleşmenizi iletiler birlikte alış verişleri hello ortağıyla göre yapılandırın. Özellik açıklamaları için bu bölümdeki hello tablolara bakın.

    **Alma ayarlarını** şu bölümlere düzenlenmiştir: tanımlayıcılar, bildirim, şemalar, denetim numaraları, doğrulama ve iç ayarlar.

    !["Alma ayarlarını" yapılandırma](./media/logic-apps-enterprise-integration-edifact/edifact-2.png)  

2. Bitirdikten sonra emin toosave ayarlarınızı seçerek olun **Tamam**.

Şimdi sözleşmenizi hazır toohandle gelen ayarları seçili tooyour uygun iletileri.

### <a name="identifiers"></a>Tanımlayıcıları

| Özellik | Açıklama |
| --- | --- |
| UNB6.1 (alıcı başvuru parola) |1 ile 14 arasında karakter arasında alfasayısal bir değer girin. |
| UNB6.2 (alıcı başvuru niteleyici) |En az bir karakter ve en çok iki karakter alfasayısal bir değer girin. |

### <a name="acknowledgments"></a>İlgili kaynaklar

| Özellik | Açıklama |
| --- | --- |
| İleti Okundu Bilgisi (CONTRL) |Bu onay kutusunu tooreturn bir teknik (CONTRL) bildirim toohello değişim gönderen seçin. Merhaba bildirim toohello değişim gönderen hello gönderme ayarları hello anlaşması için göre gönderilir. |
| Bildirim (CONTRL) |Bir işlev (CONTRL) bildirim toohello değişim gönderen hello bildirim hello gönderme ayarları hello anlaşması için temel toohello değişim gönderen gönderilen bu onay kutusunu tooreturn seçin. |

### <a name="schemas"></a>Şemalar

| Özellik | Açıklama |
| --- | --- |
| UNH2.1 (TÜR) |Bir işlem kümesi türü seçin. |
| UNH2.2 (SÜRÜM) |Merhaba ileti sürüm numarası girin. (En az, bir karakter; maksimum, üç karakter). |
| UNH2.3 (SÜRÜM) |Merhaba ileti sürüm numarası girin. (En az, bir karakter; maksimum, üç karakter). |
| UNH2.5 (İLİŞKİLİ ATANAN KODU) |Atanan hello kodu girin. (En büyük, altı karakter. Alfasayısal olmalıdır). |
| UNG2.1 (UYGULAMA GÖNDEREN KİMLİĞİ) |En az bir karakter ve en çok 35 karakter alfasayısal bir değer girin. |
| UNG2.2 (UYGULAMA GÖNDEREN KODU NİTELEYİCİSİ) |En fazla dört karakter alfasayısal bir değer girin. |
| ŞEMA |Select hello daha önce ilişkili tümleştirme hesabınızdan toouse istediğiniz şema karşıya yüklendi. |

### <a name="control-numbers"></a>Denetim numaraları
| Özellik | Açıklama |
| --- | --- |
| Değişim kontrol numarası çoğaltmaları izin verme |tooblock yinelenen etkileşimler, bu özellik seçin. Seçili hello EDIFACT kod çözme eylem alınan hello değişimi için hello değiş tokuş denetim numarası (UNB5) daha önce işlenen değiş tokuş denetim numarası eşleşmiyor denetler. Bir eşleşme algılanırsa, hello değişim işlenmez. |
| Her (days) günde bir UNB5 kopyalarını denetle |Toodisallow yinelenen değişim denetim numaraları seçerseniz, hello tooperform hello zaman denetlemek için bu ayarı hello uygun değer vererek gün sayısını belirtebilirsiniz. |
| Yinelenen Grup denetim numaralarına izin verme |Yinelenen grup denetim numaraları (UNG5) tooblock interchanges, bu özellik seçin. |
| Yinelenen İşlem kümesi denetim numaralarına izin verme |tooblock yinelenen işlem kümesi denetim sayılarla (UNH1) seçin, bu özellik interchanges. |
| EDIFACT bildirim denetim sayısı |toodesignate hello işlem referans numaraları kullanmak için bir bildirim ayarlayın, hello önek, bir dizi başvuru numarası ve bir sonek için bir değer girin. |

### <a name="validations"></a>Doğrulama

Her doğrulama satır tamamladığınızda, başka bir otomatik olarak eklenir. Herhangi bir kuralın belirtmezseniz, doğrulama hello "Varsayılan" satır kullanır.

| Özellik | Açıklama |
| --- | --- |
| İleti türü |Merhaba EDI ileti türünü seçin. |
| EDI doğrulama |EDI doğrulama hello şema EDI özellikleri, uzunluk kısıtlamaları, boş veri öğeleri ve sondaki ayırıcılar tarafından tanımlanan veri türleri gerçekleştirin. |
| Genişletilmiş Doğrulama |Merhaba veri türü değilse EDI, doğrulama üzerinde hello veri öğesi gereksinimdir ve yineleme, numaralandırmalar ve veri öğesi uzunluğu doğrulama (min/max) izin verilir. |
| Başında ve sonunda sıfır izin ver |Başında veya sonunda sıfır ek korumak ve karakterleri boşluk. Bu karakterleri kaldırmayın. |
| Başında ve sonunda sıfır kırpma |Baştaki veya sondaki sıfır ve boşluk karakterlerini Kaldır. |
| Sondaki ayırıcı İlkesi |Sondaki ayırıcılar oluşturur. <p>Seçin **izin** tooprohibit sonundaki sınırlayıcılar ve ayırıcı hello olarak alınan değişim. Merhaba değişim sonundaki sınırlayıcılar ve ayırıcılar varsa, hello değişim geçerli bildirilmedi. <p>Seçin **isteğe bağlı** tooaccept interchanges ile veya olmadan sonundaki sınırlayıcılar ve ayırıcılar. <p>Seçin **zorunlu** zaman alınan hello değişim olmalıdır sonundaki sınırlayıcılar ve ayırıcılar. |

### <a name="internal-settings"></a>İç ayarları

| Özellik | Açıklama |
| --- | --- |
| Sondaki ayırıcılara izin veriliyorsa boş XML etiketleri oluştur |Bu onay kutusunu toohave hello değişim gönderen dahil seçin ayırıcılar sondaki için XML etiketleri boş. |
| Değişimi işlem kümeleri olarak böl; hata durumunda işlem kümelerini askıya al|Merhaba uygun Zarf toohello işlem kümesi uygulayarak ayrı bir XML belge içine bir değişim kümesindeki her bir işlem ayrıştırır. Doğrulama başarısız hello işlem kümeleri askıya alın. |
| Değişimi işlem kümeleri olarak böl; hata durumunda değişimi askıya al|Merhaba uygun Zarf uygulayarak ayrı bir XML belge içine bir değişim kümesindeki her bir işlem ayrıştırır. Merhaba değişim bir veya daha fazla işlem kümelerinde doğrulama başarısız olduğunda hello tüm değişim askıya alın. | 
| Değişim korumak - işlem kümeleri askıya alma hatası |Merhaba değişim dokunmaz, hello tüm toplu değişim için bir XML belgesi oluşturur. Doğrulama başarısız hello işlem kümeleri askıya alma, diğer tüm işlem tooprocess devam ederken ayarlar. |
| Değişimi koru; hata durumunda değişimi askıya al |Merhaba değişim dokunmaz, hello tüm toplu değişim için bir XML belgesi oluşturur. Merhaba değişim bir veya daha fazla işlem kümelerinde doğrulama başarısız olduğunda hello tüm değişim askıya alın. |

## <a name="configure-how-your-agreement-sends-messages"></a>Nasıl sözleşmenizi iletileri gönderir yapılandırın

Bu anlaşma nasıl tanımlar ve bu anlaşma ile tooyour ortaklarının gönderdiği giden iletilerini işleme yapılandırabilirsiniz.

1.  Altında **Ekle**seçin **gönderme ayarları**.
İletileri ile alış verişleri ortağınızla birlikte sözleşmenize göre bu özelliklerini yapılandırın. Özellik açıklamaları için bu bölümdeki hello tablolara bakın.

    **Gönderme ayarları** şu bölümlere düzenlenmiştir: tanımlayıcılar, bildirim, şemalar, zarflar, karakter kümesi ve ayırıcılar, denetim numaraları ve doğrulama.

    !["Ayarlarını Gönder" yapılandırın](./media/logic-apps-enterprise-integration-edifact/edifact-3.png)    

2. Bitirdikten sonra emin toosave ayarlarınızı seçerek olun **Tamam**.

Seçili tooyour ayarları uygun iletileri Giden hazır toohandle sözleşmenizi sunulmuştur.

### <a name="identifiers"></a>Tanımlayıcıları

| Özellik | Açıklama |
| --- | --- |
| UNB1.2 (sözdizimi sürüm) |Arasında bir değer seçin **1** ve **4**. |
| UNB2.3 (Gönderici Ters Yönlendirme Adresi) |En az bir karakter ve en çok 14 karakter alfasayısal bir değer girin. |
| UNB3.3 (Alıcı Ters Yönlendirme Adresi) |En az bir karakter ve en çok 14 karakter alfasayısal bir değer girin. |
| UNB6.1 (alıcı başvuru parola) |Bir en az ve en çok 14 karakter alfasayısal bir değer girin. |
| UNB6.2 (alıcı başvuru niteleyici) |En az bir karakter ve en çok iki karakter alfasayısal bir değer girin. |
| UNB7 (uygulama başvuru kimliği) |En az bir karakter ve en çok 14 karakter alfasayısal bir değer girin |

### <a name="acknowledgment"></a>Bildirim
| Özellik | Açıklama |
| --- | --- |
| İleti Okundu Bilgisi (CONTRL) |Barındırılan hello ortağı tooreceive teknik (CONTRL) bildirim görüyorsa bu onay kutusunu seçin. Bu ayar hello iletisi gönderiyor, bu barındırılan hello ortağı belirtir hello Konuk ortağından onay ister. |
| Bildirim (CONTRL) |Barındırılan hello ortağı tooreceive bir işlev (CONTRL) bildirim görüyorsa bu onay kutusunu seçin. Bu ayar hello iletisi gönderiyor, bu barındırılan hello ortağı belirtir hello Konuk ortağından onay ister. |
| Kabul edilen işlem kümeleri için SG1/SG4 döngüsü oluştur |İşlev bildirim toorequest seçerseniz, bu onay kutusunu tooforce oluşturma SG1/SG4 döngüsü kabul edilen işlem kümeleri için işlevsel CONTRL ilgili kaynaklar seçin. |

### <a name="schemas"></a>Şemalar
| Özellik | Açıklama |
| --- | --- |
| UNH2.1 (TÜR) |Bir işlem kümesi türü seçin. |
| UNH2.2 (SÜRÜM) |Merhaba ileti sürüm numarası girin. |
| UNH2.3 (SÜRÜM) |Merhaba ileti sürüm numarası girin. |
| ŞEMA |Merhaba şema toouse seçin. Şemalar tümleştirme hesabınızda bulunur. tooaccess, şemalar tümleştirme hesap tooyour mantıksal uygulamanızı ilk bağlantı. |

### <a name="envelopes"></a>Zarflar
| Özellik | Açıklama |
| --- | --- |
| UNB8 (öncelik kodu işleme) |Birden fazla karakter uzunluğunda değil alfabetik bir değer girin. |
| UNB10 (iletişimi sözleşme) |En az bir karakter ve en çok 40 karakter alfasayısal bir değer girin. |
| UNB11 (Test göstergesi) |Test verileri oluşturulan değişim hello bu onay kutusunu tooindicate seçin |
| UNA Segmentini Uygula (Hizmet Dize Önerisi) |Bu onay kutusunu toogenerate UNA segment gönderilen hello değişim toobe için seçin. |
| UNG Segmentlerini Uygula (İşlev Grubu Üstbilgisi) |Bu onay kutusunu toocreate hello işlevsel grup üstbilgisi hello gönderilen iletileri toohello Konuk ortağında segmentlerinde gruplandırma seçin. Merhaba aşağıdaki değerler kullanılan toocreate hello UNG kesimleri şunlardır: <p>İçin **UNG1**, en az bir karakter ve en fazla altı karakter alfasayısal bir değer girin. <p>İçin **UNG2.1**, en az bir karakter ve en çok 35 karakter alfasayısal bir değer girin. <p>İçin **UNG2.2**, en fazla dört karakter alfasayısal bir değer girin. <p>İçin **UNG3.1**, en az bir karakter ve en çok 35 karakter alfasayısal bir değer girin. <p>İçin **UNG3.2**, en fazla dört karakter alfasayısal bir değer girin. <p>İçin **UNG6**, aşağıdakilerden en az ve en çok üç karakter alfasayısal bir değer girin. <p>İçin **UNG7.1**, en az bir karakter ve en çok üç karakter alfasayısal bir değer girin. <p>İçin **UNG7.2**, en az bir karakter ve en çok üç karakter alfasayısal bir değer girin. <p>İçin **UNG7.3**, en az 1 karakter ve en çok 6 karakter alfasayısal bir değer girin. <p>İçin **UNG8**, en az bir karakter ve en çok 14 karakter alfasayısal bir değer girin. |

### <a name="character-sets-and-separators"></a>Karakter Kümeleri ve Ayırıcılar

Merhaba karakter kümesi dışında her ileti türü için kullanılan sınırlayıcıları toobe farklı bir dizi girebilirsiniz. Karakter kümesi için belirli bir ileti şeması belirtilmezse, hello varsayılan karakter kümesini kullanılır.

| Özellik | Açıklama |
| --- | --- |
| UNB1.1 (sistem tanımlayıcısı) |Select hello EDIFACT karakter değişim giden hello üzerinde uygulanan toobe ayarlayın. |
| Şema |Bir şema hello aşağı açılan listeden seçin. Her satır tamamladıktan sonra yeni bir satır otomatik olarak eklenir. Merhaba seçili şeması ayırıcı açıklamaları aşağıdaki hello üzerinde temel toouse istediğiniz select hello ayırıcılar ayarlayın. |
| Giriş türü |Bir input type hello aşağı açılan listeden seçin. |
| Bileşen ayırıcı |tooseparate bileşik veri öğeleri, tek bir karakter girin. |
| Veri öğesi ayırıcı |bileşik veri öğeleri içindeki tooseparate basit veri öğelerinin tek bir karakter girin. |
| Segment Sonlandırıcı |tooindicate hello bir EDI segmentinin sonunu tek bir karakter girin. |
| Son eki |Merhaba segment tanımlayıcı ile kullanılan hello karakteri seçin. Bir son eki atayın ve yeniden hello segment Sonlandırıcı veri öğesi boş olabilir. Merhaba segment sonlandırıcı boş bırakılırsa, sonek atamanız gerekir. |

### <a name="control-numbers"></a>Denetim numaraları
| Özellik | Açıklama |
| --- | --- |
| UNB5 (değişim kontrol numarası) |Bir önek, değerleri hello Değişim Denetimi numarası için bir aralığı ve bir sonek girin. Bu kullanılan toogenerate giden bir değişim değerlerdir. Merhaba denetim numarası ederken hello önek ve sonek isteğe bağlıdır. Merhaba denetim sayısı, her yeni ileti artırılır; Merhaba önek ve sonek kalır hello aynı. |
| UNG5 (Grup denetim sayısı) |Bir önek, değerleri hello Değişim Denetimi numarası için bir aralığı ve bir sonek girin. Bu değerler kullanılır toogenerate hello grubu denetim sayısı. Merhaba denetim numarası ederken hello önek ve sonek isteğe bağlıdır. Hello en büyük değerine ulaşılana kadar hello denetim sayısı için her yeni ileti artırılır; Merhaba önek ve sonek kalır hello aynı. |
| UNH1 (ileti üstbilgisi başvuru numarası) |Bir önek, değerleri hello Değişim Denetimi numarası için bir aralığı ve bir sonek girin. Bu değerler kullanılır toogenerate hello ileti üstbilgisi başvuru numarası. Merhaba başvuru numarası ederken hello önek ve sonek isteğe bağlıdır. Merhaba başvuru numarası yeni her ileti için artırılır; Merhaba önek ve sonek kalır hello aynı. |

### <a name="validations"></a>Doğrulama

Her doğrulama satır tamamladığınızda, başka bir otomatik olarak eklenir. Herhangi bir kuralın belirtmezseniz, doğrulama hello "Varsayılan" satır kullanır.

| Özellik | Açıklama |
| --- | --- |
| İleti türü |Merhaba EDI ileti türünü seçin. |
| EDI doğrulama |EDI doğrulama hello şema, uzunluk kısıtlamaları, boş veri öğeleri ve sondaki ayırıcılar hello EDI özellikleri tarafından tanımlanan veri türleri gerçekleştirin. |
| Genişletilmiş Doğrulama |Merhaba veri türü değilse EDI, doğrulama üzerinde hello veri öğesi gereksinimdir ve yineleme, numaralandırmalar ve veri öğesi uzunluğu doğrulama (min/max) izin verilir. |
| Başında ve sonunda sıfır izin ver |Başında veya sonunda sıfır ek korumak ve karakterleri boşluk. Bu karakterleri kaldırmayın. |
| Başında ve sonunda sıfır kırpma |Baştaki veya sondaki sıfır karakterleri kaldırın. |
| Sondaki ayırıcı İlkesi |Sondaki ayırıcılar oluşturur. <p>Seçin **izin** tooprohibit sonundaki sınırlayıcılar ve ayırıcı hello olarak gönderilen değişim. Merhaba değişim sonundaki sınırlayıcılar ve ayırıcılar varsa, hello değişim geçerli bildirilmedi. <p>Seçin **isteğe bağlı** toosend interchanges ile veya olmadan sonundaki sınırlayıcılar ve ayırıcılar. <p>Seçin **zorunlu** gönderilen hello değişim sonundaki sınırlayıcılar ve ayırıcıları kullanmanız gerekiyorsa. |

## <a name="find-your-created-agreement"></a>Oluşturulan sözleşmenizi Bul

1.  Merhaba üzerinde anlaşma özelliklerinizi ayarlama işlemini tamamladıktan sonra **Ekle** dikey penceresinde, seçin **Tamam** toofinish sözleşmesi ve dönüş tooyour tümleştirme hesabı dikey oluşturma.

    Yeni eklenen sözleşmenizi artık görünür, **anlaşmaları** listesi.

2.  Ayrıca, tümleştirme hesabına genel bakış sözleşmelerinizi görüntüleyebilirsiniz. Tümleştirme hesabı dikey penceresinde, seçin **genel bakış**seçeneğini belirleyip hello **anlaşmaları** döşeme. 

    ![Tüm Anlaşmalar "Anlaşmaları" döşeme tooview seçin](./media/logic-apps-enterprise-integration-edifact/edifact-4.png)   

## <a name="view-swagger-file"></a>Görünüm Swagger dosyası
tooview hello Swagger hello EDIFACT bağlayıcı ayrıntılarını görmek [EDIFACT](/connectors/edifact/).

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")  

