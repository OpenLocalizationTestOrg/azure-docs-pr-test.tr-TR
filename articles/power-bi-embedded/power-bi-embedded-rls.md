---
title: "Power BI Embedded ile aaaRow düzeyinde güvenlik"
description: "Satır düzeyi güvenlik Power BI Embedded ile ilgili ayrıntıları"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Power BI Embedded ile satır düzeyinde güvenlik

Satır düzeyi güvenlik (RLS), rapor veya birden çok farklı kullanıcılar toouse hello için tüm görme farklı veriler aynı rapor veren veri kümesi içinde kullanılan toorestrict kullanıcı erişimi tooparticular veri olabilir. Power BI Embedded artık RLS ile yapılandırılmış veri kümelerini destekler.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

Sipariş tootake avantajlarından RLS, üç ana kavramı anlamak önemlidir; Kullanıcıları, rolleri ve kuralları. Her daha yakın bir göz atalım:

**Kullanıcıların** – bu hello gerçek son kullanıcılar görüntülemekte olduğunuz raporlar. Power BI Embedded içinde kullanıcıların bir uygulama belirteci hello username özelliği tarafından tanımlanır.

**Rolleri** – kullanıcılar tooroles aittir. Bir rolü kuralları için bir kapsayıcı ve bir şey "Satış Yöneticisi" veya "Satış Temsilcisi" gibi adlandırılabilir. Power BI Embedded içinde kullanıcıların bir uygulama belirteci hello roller özelliği tarafından tanımlanır.

**Kuralları** – rollerin kurallar vardır ve uygulanan toobe toohello veri giderek hello gerçek filtreler bu kurallardır. Bu kadar basit olabilir "Ülke = tr" veya daha fazla dinamik bir şey.

### <a name="example"></a>Örnek

Bu makalede Hello kalanı için RLS yazma ve, katıştırılmış bir uygulama içinde kullanma örneği sağlarız. Bizim örneğimizde hello kullanan [Retail Analysis örnek](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX dosyası.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

Retail Analysis örneğimizde bir belirli perakende zincirindeki tüm hello depoları için satış gösterir. RLS, olmadan hangi bölge olsun Yöneticisi oturum açtığında ve görünümler rapor Merhaba, bunlar görürsünüz aynı veri hello. Üst düzey yönetim her bölge yöneticisi yalnızca hello satışlarının yönettikleri hello depoları ve toodo bu görmelisiniz belirledi, RLS kullanırız.

RLS, Power BI Desktop'ta yazılmıştır. Merhaba veri kümesini ve raporu açıldığında, biz toodiagram görünüm toosee hello şema geçebilirsiniz:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

Bu şema ile birkaç şey toonotice şunlardır:

* Tüm ölçüleri, ister **toplam satış**, hello depolanan **satış** Olgu Tablosu.
* Dört ek ilgili boyut tabloları vardır: **öğesi**, **zaman**, **deposu**, ve **bölgesi**.
* Merhaba okları hello ilişki satırlarındaki filtreleri bir tablo tooanother akabilir hangi yolu belirtin. Örneğin, bir filtre yerleştirildiği **zaman [Date]**, hello geçerli şemada, yalnızca hello değerlerde aşağı filtreler **satış** tablo. Başka bir tablo tüm hello okları hello ilişki satırları noktası toohello satış tablosuna ve değil hemen bu filtrenin etkilenecek.
* Merhaba **bölge** tablo her bölge için hello yöneticisi olan gösterir:
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

Biz filtre toohello uygularsanız bu şemaya göre **bölge yöneticisi** sütununda bölge tablo hello ve bu filtre hello raporu görüntüleme hello kullanıcı eşleşiyorsa, bu filtre da hello filtre **deposu**ve **satış** tabloları tooonly Yöneticisi bu belirli bölge verilerini gösterir.

İşte nasıl:

1. Merhaba modelleme sekmesinde, **Rolleri Yönet**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. Adlı yeni bir rol oluşturmak **Yöneticisi**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. Merhaba, **bölge** tablo DAX ifadesi aşağıdaki hello girin: **[Bölge Yöneticisi] USERNAME() =**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. toomake emin hello kuralları çalıştığınız, üzerinde hello **modelleme** sekmesini tıklatın, **görünüm rolleri olarak**ve ardından hello aşağıdakileri girin:  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   olarak oturum gibi varsa hello raporları şimdi veri gösterir **Barış Ma**.

Merhaba filtre, burada yaptığımız hello şekilde uygulama filtre uygulayarak hello tüm kayıtları aşağı **bölge**, **deposu**, ve **satış** tabloları. Ancak, hello filtre yönünü arasındaki hello ilişkileri nedeniyle **satış** ve **zaman**, **satış** ve **öğesi**ve **Öğesi** ve **zaman** tabloları aşağı filtrelenmez.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

Bu gereksinim için Tamam olabilir, bunlar Satış yok yöneticileri toosee öğeleri de istemiyorsanız, ancak biz her iki yönde hello ilişkisi ve akış hello güvenlik filtresi için çapraz filtreleme çift yönlü Aç. Bu hello ilişkisi düzenleyerek yapılabilir **satış** ve **öğesi**, şöyle:

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

Şimdi, filtreleri hello satış tablo toohello ayrıca akabilir **öğesi** tablosu:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> Verileriniz için DirectQuery modu kullanıyorsanız, tooenable çift yönlü-arası bu iki seçenek seçerek filtreleme gerekir:

1. **Dosya** -> **seçenekleri ve ayarları** -> **Önizleme özellikleri** -> **çapraz için her iki yönde filtreleme etkinleştir DirectQuery**.
2. **Dosya** -> **seçenekleri ve ayarları** -> **DirectQuery** -> **DirectQuerymodundaKısıtlanmamışölçüizinver**.

çift yönlü çapraz filtreleme, indirme hello hakkında daha fazla toolearn [çift yönlü çapraz filtreleme SQL Server Analysis Services 2016 ve Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) teknik incelemesi.

Bu Power BI Desktop'ta bitti toobe gereken tüm hello iş yukarı sarmalar, ancak bir daha fazla parça bitti toobe toomake gereken çalışmanın yok hello RLS kuralları tanımladığımız iş Power BI Embedded içinde. Kullanıcıların kimlik doğrulaması ve uygulamanız tarafından yetkili ve uygulama belirteçleri kullanılan toogrant olduğundan, kullanıcı erişim tooa belirli Power BI Embedded rapor. Power BI Embedded kullanıcı kim herhangi bir özel bilgi yok. RLS toowork için uygulama belirtecinin bir parçası bazı ek bağlam toopass gerekir:

* **Kullanıcı adı** (isteğe bağlı) – RLS ile kullanılan bu kullanılabilecek bir dizedir toohelp RLS kuralları uygularken hello kullanıcı tanımlayın. Bkz. satır düzeyi güvenlikte Power BI Embedded kullanma
* **rolleri** – satır düzeyi güvenlik kuralları uygularken hello rolleri tooselect içeren bir dize. Birden fazla rol geçirilirse, bir dize dizisi olarak aktarılmalıdır.

Hello kullanarak hello belirteci oluşturma [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) yöntemi. Merhaba username özelliği varsa, ayrıca en az bir değer rollerinde geçmesi gerekir.

Örneğin, hello EmbedSample değiştirebilirsiniz. Gelen DashboardController satır 55 güncelleştirilemedi

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

-

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

Merhaba tam uygulama belirteci şunun gibi görünür:

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

Birisi Bu rapor, uygulama tooview açtığında artık, tüm hello parça ile birlikte, yalnızca mümkün toosee hello veri toosee, izin verilen bizim satır düzeyi güvenlik tarafından tanımlandığı şekilde olmaları.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>Ayrıca bkz.

[Satır düzeyi güvenlik (RLS) güç](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Örnek Ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)

