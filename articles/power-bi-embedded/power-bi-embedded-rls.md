---
title: "Power BI Embedded ile satır düzeyi güvenliği"
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
ms.openlocfilehash: 1cde5b9ee4c716af07d427d4d0eb3f0775d456ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Power BI Embedded ile satır düzeyinde güvenlik

Satır düzeyi güvenlik (RLS), rapor veya veri kümesi, birden çok farklı kullanıcıların aynı raporun tüm görme farklı veriler kullanmasına izin vermeyi içinde belirli veri kullanıcı erişimi sınırlamak için kullanılabilir. Power BI Embedded artık RLS ile yapılandırılmış veri kümelerini destekler.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

RLS yararlanmak için üç ana kavramı anlamak önemlidir; Kullanıcıları, rolleri ve kuralları. Her daha yakın bir göz atalım:

**Kullanıcıların** – Bu gerçek son kullanıcılar görüntülemekte olduğunuz raporlar. Power BI Embedded içinde kullanıcıların bir uygulama belirteci username özelliği tarafından tanımlanır.

**Rolleri** – kullanıcıları rollere ait. Bir rolü kuralları için bir kapsayıcı ve bir şey "Satış Yöneticisi" veya "Satış Temsilcisi" gibi adlandırılabilir. Power BI Embedded içinde kullanıcıların bir uygulama belirteci roller özelliği tarafından tanımlanır.

**Kuralları** – rollerin kurallar vardır ve verilere uygulanacak giderek gerçek filtreler bu kurallardır. Bu kadar basit olabilir "Ülke = tr" veya daha fazla dinamik bir şey.

### <a name="example"></a>Örnek

Bu makalede kalanı için RLS yazma ve, katıştırılmış bir uygulama içinde kullanma örneği sağlarız. Bizim örneğimizde kullanan [Retail Analysis örnek](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX dosyası.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

Retail Analysis örneğimizde bir belirli perakende zincirindeki tüm depoları için satış gösterir. Hangi bölge olsun Yöneticisi oturum açtığında ve rapor görünümleri RLS, bunlar aynı verileri görürsünüz. Üst düzey yönetim her bölge yöneticisi yalnızca satış yönettikleri depolarının görmeniz gerekir ve bunu yapmak için biz RLS kullanabilirsiniz belirledi.

RLS, Power BI Desktop'ta yazılmıştır. Rapor ve veri kümesi açıldığında, biz şema görmek için diyagram görünümüne geçiş yapabilirsiniz:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

Bu şema ile fark birkaç şunlardır:

* Tüm ölçüleri, ister **toplam satış**, depolanmış **satış** Olgu Tablosu.
* Dört ek ilgili boyut tabloları vardır: **öğesi**, **zaman**, **deposu**, ve **bölgesi**.
* İlişki satırlarındaki okları filtreleri başka bir tablodan akış hangi yolu belirtin. Örneğin, bir filtre yerleştirildiği **zaman [Date]**, geçerli şemada, yalnızca değerleri aşağı filtreler **satış** tablo. Tüm okları ilişki satırlarındaki satış tabloya ve değil hemen noktası bu yana başka bir tablo bu filtrenin etkilenecek.
* **Bölge** tablo her bölge için yöneticisi olan gösterir:
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

Biz bir filtre uygularsanız, bu şemaya göre **bölge yöneticisi** bölge tablodaki sütun ve bu filtre raporu görüntüleme kullanıcı eşleşiyorsa, bu filtre da aşağı süzer **deposu** ve  **Satış** yalnızca tablolara Yöneticisi bu belirli bölge verilerini gösterir.

İşte nasıl:

1. Modelleme sekmesinde, **Rolleri Yönet**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. Adlı yeni bir rol oluşturmak **Yöneticisi**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. İçinde **bölge** tablo aşağıdaki DAX ifadesi girin: **[Bölge Yöneticisi] USERNAME() =**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. Kuralları çalıştığınız, üzerinde emin olmak için **modelleme** sekmesini tıklatın, **görünüm rolleri olarak**ve ardından aşağıdakileri girin:  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   Sanki olarak imzalanmış raporlar artık verileri Göster **Barış Ma**.

Burada, yaptığımız şekilde filtre uygulama filtre uygulayarak tüm kayıtları aşağı **bölge**, **deposu**, ve **satış** tabloları. Ancak, filtre yönünü arasındaki ilişkileri nedeniyle **satış** ve **zaman**, **satış** ve **öğesi**ve **Öğesi** ve **zaman** tabloları aşağı filtrelenmez.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

Bu gereksinim için Tamam olabilir, ancak bunlar Satış yok öğeleri görmek için yöneticileri olmasını istemezseniz, biz çift yönlü çapraz filtreleme ilişkisi için açın ve her iki yönde güvenlik filtresi akış. Bu arasındaki ilişkiyi düzenleyerek yapılabilir **satış** ve **öğesi**, şöyle:

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

Şimdi, filtreleri Ayrıca satış tablosundan akabilir **öğesi** tablosu:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> Verileriniz için DirectQuery modu kullanıyorsanız, bu iki seçenek seçerek çift yönlü çapraz filtreleme etkinleştirmeniz gerekir:

1. **Dosya** -> **seçenekleri ve ayarları** -> **Önizleme özellikleri** -> **çapraz için her iki yönde filtreleme etkinleştir DirectQuery**.
2. **Dosya** -> **seçenekleri ve ayarları** -> **DirectQuery** -> **DirectQuerymodundaKısıtlanmamışölçüizinver**.

Çift yönlü çapraz filtreleme hakkında daha fazla bilgi için indirme [çift yönlü çapraz filtreleme SQL Server Analysis Services 2016 ve Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) teknik incelemesi.

Bu Power BI Desktop'ta yapılması gereken tüm iş yukarı sarmalar, ancak iş biz Power BI Embedded içinde tanımlanan bir daha fazla parça of RLS hale getirilmesi için gereken iş kuralları yok. Kullanıcıların kimlik doğrulaması ve uygulamanız tarafından yetkili ve uygulama belirteçleri, belirli bir Power BI Embedded rapor kullanıcı erişimi vermek için kullanılır. Power BI Embedded kullanıcı kim herhangi bir özel bilgi yok. Çalışmak RLS için uygulama belirtecinin bir parçası bazı ek bağlam geçmesi gerekir:

* **Kullanıcı adı** (isteğe bağlı) – RLS ile kullanılan bu RLS kuralları uygularken kullanıcı tanımlamaya yardımcı olmak için kullanılan bir dize değeridir. Bkz. satır düzeyi güvenlikte Power BI Embedded kullanma
* **rolleri** – satır düzeyi güvenlik kuralları uygularken seçmek için rolleri içeren bir dize. Birden fazla rol geçirilirse, bir dize dizisi olarak aktarılmalıdır.

Kullanarak belirteci oluşturma [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) yöntemi. Username özelliği varsa, ayrıca en az bir değer rollerinde geçmesi gerekir.

Örneğin, EmbedSample değiştirebilirsiniz. Gelen DashboardController satır 55 güncelleştirilemedi

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

-

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

Tam uygulama belirteci şunun gibi görünür:

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

Birisi bu raporu görüntülemek için uygulamamıza açtığında artık, tüm parçaları ile birlikte, bunlar yalnızca bunlar görmek için bizim satır düzeyi güvenlik tarafından tanımlanan izin verilen verileri görmek kavrayabilirsiniz.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>Ayrıca bkz.

[Satır düzeyi güvenlik (RLS) güç](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Örnek Ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Başka sorunuz mu var? [Power BI Topluluğu'nu deneyin](http://community.powerbi.com/)

