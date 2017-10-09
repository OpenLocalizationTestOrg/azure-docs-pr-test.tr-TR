---
title: "aaaManage veritabanı rolleri ve kullanıcıların Azure Analysis Services | Microsoft Docs"
description: "Toomanage nasıl veritabanı rolleri ve kullanıcıların Azure Analysis Services sunucusunda öğrenin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a>Veritabanı rolleri ve kullanıcıları yönetme

Merhaba model veritabanı düzeyinde tüm kullanıcılar tooa rolüne ait olması gerekir. Rolleri hello model veritabanı için belirli izinlerine sahip olan kullanıcıların tanımlar. Herhangi bir kullanıcı veya güvenlik grubu tooa rol hello Azure AD kiracısında içinde bir hesap olmalıdır eklenen hello sunucusu olarak aynı abonelik.

Rolleri tanımlama nasıl kullandığınız hello aracını kullanarak farklı bağlı olarak olmakla birlikte, hello etkisi aynı hello olduğu.

Rol izinleri şunlardır:
*  **Yönetici** -kullanıcınız hello veritabanı için tam izinleri. Yönetici izinlerine sahip veritabanı rolleri, sunucu yöneticisinden farklıdır.
*  **İşlem** -kullanıcıların tooand bağlanabilir hello veritabanında işlem işlemleri gerçekleştirmek ve model veritabanı verileri analiz etmek.
*  **Okuma** -kullanıcılar, bir istemci kullanabilir uygulama tooconnect tooand model veritabanı verileri analiz edin.

Tablo modeli projesi oluştururken, rolleri oluşturun ve SSDT içinde rol Yöneticisi'ni kullanarak kullanıcıları veya grupları toothose roller ekleyin. Dağıtılan tooa server kullandığınızda SSMS, [Analiz Hizmetleri PowerShell cmdlet'leri](https://msdn.microsoft.com/library/hh758425.aspx), veya [tablolu modeli komut dosyası dili](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd veya rollerini ve kullanıcı üyeleri kaldırın.

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a>tooadd veya roller ve SSDT kullanıcıları yönetin  
  
1.  Ssdt'de > **tablolu Model Gezgini**, sağ **rolleri**.  
  
2.  **Rol Yöneticisi**'nde **Yeni**'ye tıklayın.  
  
3.  Merhaba rol için bir ad yazın.  
  
     Varsayılan olarak, hello hello varsayılan rol adını artımlı olarak her yeni rol için numaralandırılır. Merhaba üye türü, örneğin, finans yöneticileri veya İnsan Kaynakları uzmanlarıyla açıkça tanımlayan bir ad yazın önerilir.  
  
4.  Aşağıdaki izinleri hello birini seçin:  
  
    |İzin|Açıklama|  
    |----------------|-----------------|  
    |**Yok**|Üyeleri hello model şeması değişiklik yapılamaz ve veri sorgulanamıyor.|  
    |**Okuma**|Üyeler (satır filtreleri bağlı olarak) verileri sorgulayabilir ancak hello model şeması değiştiremezsiniz.|  
    |**Okuma ve işlem**|Üye verileri (temel alınarak satır düzeyi filtreleri) ve çalıştırma işlemi ve işlem tüm işlemleri sorgulama yapabilirsiniz ancak hello model şeması değiştiremezsiniz.|  
    |**İşlem**|Üye işlemi ve işlem tüm işlemleri çalıştırabilirsiniz. Merhaba model şeması değişiklik yapılamaz ve veri sorgulayamıyor.|  
    |**Yönetici**|Üyeleri hello model şeması değiştirmek ve tüm verileri sorgulayabilirsiniz.|   
  
5.  Merhaba rol kullanıyorsanız oluşturma okuma veya okuma ve işlem izni bir DAX formülü kullanarak satır filtrelerini ekleyebilirsiniz. Merhaba tıklatın **satır filtrelerini** sekmesinde, bir tablo seçin, sonra hello tıklatın **DAX filtre** alan ve bir DAX formülü girin.
  
6.  Tıklatın **üyeleri** > **dış eklemek**.  
  
8.  İçinde **dış Üye Ekle**, kullanıcıları veya grupları, Azure AD kiracınızda tarafından e-posta adresi girin. Tamam'ı tıklatın ve Rol Yöneticisi'ni kapatın rolleri ve Rol üyeleri tablolu Model Gezgini'nde görünür. 
 
     ![Rol ve kullanıcı tablolu Model Gezgini](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. Tooyour Azure Analysis Services sunucusuna dağıtın.


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a>tooadd veya roller ve SSMS kullanıcıları yönetin
tooadd rol ve kullanıcı tooa model veritabanı dağıtıldı, bağlı toohello server sunucu yöneticisi olarak veya zaten bir veritabanı rolü yönetici izinlerine sahip olması gerekir.

1. Nesne Exporer içinde sağ **rolleri** > **yeni rol**.

2. İçinde **Rol Oluştur**, bir rol adı ve açıklama girin.

3. Bir izin seçin.
   |İzin|Açıklama|  
   |----------------|-----------------|  
   |**Tam Denetim (Yönetici)**|Üyeleri hello model şeması değiştirebilirsiniz işlemek ve tüm verileri sorgulayabilir.| 
   |**İşlem veritabanı**|Üye işlemi ve işlem tüm işlemleri çalıştırabilirsiniz. Merhaba model şeması değişiklik yapılamaz ve veri sorgulayamıyor.|  
   |**Okuma**|Üyeler (satır filtreleri bağlı olarak) verileri sorgulayabilir ancak hello model şeması değiştiremezsiniz.|  
  
4. Tıklatın **üyelik**, sonra bir kullanıcı veya grubu girin kiracınızda Azure AD tarafından e-posta adresi.

     ![Kullanıcı ekle](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. Oluşturmakta olduğunuz hello rol okuma iznine sahipse, bir DAX formülü kullanarak satır filtrelerini ekleyebilirsiniz. Tıklatın **satır filtrelerini**, bir tablo seçin ve ardından bir DAX formülü hello yazın **DAX filtre** alan. 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a>tooadd roller ve TMSL komut dosyası kullanarak kullanıcılar
Bir TMSL komut penceresinde hello XMLA SSMS veya PowerShell kullanarak çalıştırabilirsiniz. Kullanım hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) komut ve hello [rolleri](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) nesnesi.

**Örnek TMSL komut dosyası**

Bu örnekte, B2B dış kullanıcı ve Grup hello SalesBI veritabanı için Okuma izinlerine sahip toohello analist rol eklenir. Hem de dış kullanıcı hello ve Grup aynı Kiracı Azure AD olmalıdır.

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a>tooadd roller ve PowerShell kullanarak kullanıcılar
Merhaba [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) modül tablolu modeli komut dosyası dili (TMSL) sorgu veya betik kabul görev özgü veritabanı yönetimi cmdlet'leri ve hello genel amaçlı Invoke-ASCmd cmdlet'i sağlar. cmdlet aşağıdaki hello veritabanı rolleri ve kullanıcıları yönetmek için kullanılır.
  
|Cmdlet|Açıklama|
|------------|-----------------| 
|[Ekleme RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Üye tooa veritabanı rolü ekleyin.| 
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Üye veritabanı rolden kaldırır.|   
|[Çağırma ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|TMSL betiğini yürütün.|

## <a name="row-filters"></a>Satır filtreleri  
Hangi satır bir tablodaki belirli bir rol üyeleri tarafından sorgulanabilir satır filtrelerini tanımlayın. Satır filtrelerini DAX formülleri kullanarak modeldeki her tablo için tanımlanır.  
  
Satır filtreleri, yalnızca rollerini okuma ve okuma için tanımlanabilir ve işlem izinleri. Belirli bir tablo için bir satır filtresi tanımlı değilse, varsayılan olarak, başka bir tablodan çapraz filtreleme uygulanır sürece hello tablodaki tüm satırları üyeleri sorgulayabilirsiniz.
  
 Satır filtrelerini tooa TRUE/FALSE değeri, bu özel rolü üyeleri tarafından sorgulanan toodefine hello satırları değerlendirilmelidir bir DAX formülü gerektirir. Merhaba DAX formülü dahil edilmeyen satırları sorgulanamıyor. Örneğin, Müşteriler tablosu satır filtre ifadesi, aşağıdaki hello ile Merhaba *müşteriler [Country] = "ABD" =*, hello satış rolünün üyeleri yalnızca hello ABD müşteriler bakın.  
  
Satır Filtreleri Uygula belirtilen toohello satırları ve ilişkili satırları. Bir tabloda birden çok ilişki olduğunda, güvenlik etkin hello ilişki için filtre uygulayın. Satır filtrelerini diğer satır filtreleri ilişkili tablolar için örneğin tanımlanmış kesiştiğinden:  
  
|Tablo|DAX ifadesi|  
|-----------|--------------------|  
|Bölge|= Bölge [Country] = "Tr"|  
|ProductCategory|= ProductCategory [Name] "Bisiklet" =|  
|İşlemler|= İşlemleri [yıl] 2016 =|  
  
 Merhaba net üyeleri burada hello müşteri hello ABD'de, bisiklet hello ürün kategorisi olan ve hello yıl 2016 veri satırı sorgulayabilirsiniz etkisidir. Kullanıcılar, bu izinler veren başka bir rolün üyesi olmadığı sürece olmayan bisiklet ya da işlemleri 2016'da değil işlemleri işlemleri hello ABD dışında sorgulayamıyor.
  
 Merhaba filtre kullanabilirsiniz *=FALSE()*, tüm bir tabloyu için toodeny erişim tooall sıralar.

## <a name="next-steps"></a>Sonraki adımlar
  [Sunucu yöneticileri yönetin](analysis-services-server-admins.md)   
  [Azure Analysis Services PowerShell ile yönetme](analysis-services-powershell.md)  
  [Tablo modeli komut dosyası dili (TMSL) başvurusu](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

