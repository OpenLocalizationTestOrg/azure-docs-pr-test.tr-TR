---
title: "aaaWorkflow tanımlama dili şema - Azure Logic Apps | Microsoft Docs"
description: "İş akışları için Azure Logic Apps Hello iş akışı tanımı şemasını temel alan tanımlayın"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 26c94308-aa0d-4730-97b6-de848bffff91
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: f12440e9ca269a9236132deeb888dbde7fb734d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-definition-language-schema-for-azure-logic-apps"></a>Azure mantıksal uygulamaları için iş akışı tanımlama dili şeması

Bir iş akışı tanımı mantıksal uygulamanızı bir parçası olarak yürüten hello gerçek mantığını içerir. Bu tanımı, bir veya daha fazla hello mantıksal uygulama Başlat tetikleyiciler ve hello mantığı uygulama tootake için bir veya daha fazla eylemleri içerir.  
  
## <a name="basic-workflow-definition-structure"></a>Temel iş akışı tanımı yapısı

Bir iş akışı tanımı temel yapısını hello şöyledir:  
  
```json
{
    "$schema": "<schema-of the-definition>",
    "contentVersion": "<version-number-of-definition>",
    "parameters": { <parameter-definitions-of-definition> },
    "triggers": [ { <definition-of-flow-triggers> } ],
    "actions": [ { <definition-of-flow-actions> } ],
    "outputs": { <output-of-definition> }
}
```
  
> [!NOTE]
> Merhaba [iş akışı yönetimi REST API](https://docs.microsoft.com/rest/api/logic/workflows) belgelerine sahip hakkında bilgi toocreate ve logic app iş akışlarını yönetme.
  
|Öğe adı|Gerekli|Açıklama|  
|------------------|--------------|-----------------|  
|$schema|Hayır|Merhaba tanımlama dili hello sürümü açıklanmaktadır hello JSON şema dosyası Hello konumunu belirtir. Bu konum, bir tanım dışarıdan başvurduğunuzda gereklidir. Bu belge için başlangıç konumu şudur: <p>`https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#`|  
|contentVersion|Hayır|Merhaba tanımı sürümünü belirtir. Merhaba tanımı kullanarak bir iş akışı dağıttığınızda, bu değer toomake hello sağ tanımı kullanıldığından emin kullanabilirsiniz.|  
|Parametreleri|Hayır|Parametreleri tooinput veri hello tanımı içinde kullanılan belirtir. En fazla 50 parametreleri tanımlanabilir.|  
|Tetikleyicileri|Hayır|Merhaba iş akışını başlatmak hello Tetikleyicileri bilgilerini belirtir. En fazla 10 Tetikleyicileri tanımlanabilir.|  
|Eylemler|Hayır|Merhaba akışı yürütür olarak gerçekleştirilen eylemler belirtir. En fazla 250 Eylemler tanımlanabilir.|  
|Çıkışları|Hayır|Dağıtılan hello kaynak hakkındaki bilgileri belirtir. En fazla 10 çıkışları tanımlanabilir.|  
  
## <a name="parameters"></a>Parametreler

Bu bölümde kullanılan tüm hello parametreleri hello iş akışı tanımını dağıtım süresini belirtir. Hello tanımı diğer bölümlerinde kullanılabilmesi için önce bu bölümdeki tüm parametreleri bildirilmesi gerekir.  
  
Merhaba aşağıdaki örnekte bir parametrenin tanımını hello yapısını gösterir:  

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": <default-value-of-parameter>,
        "allowedValues": [ <array-of-allowed-values> ],
        "metadata" : { "key": { "name": "value"} }
    }
}
```

|Öğe adı|Gerekli|Açıklama|  
|------------------|--------------|-----------------|  
|type|Evet|**Tür**: dize <p> **Bildirim**:`"parameters": {"parameter1": {"type": "string"}` <p> **Belirtimi**:`"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Tür**: securestring <p> **Bildirim**:`"parameters": {"parameter1": {"type": "securestring"}}` <p> **Belirtimi**:`"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Tür**: int <p> **Bildirim**:`"parameters": {"parameter1": {"type": "int"}}` <p> **Belirtimi**:`"parameters": {"parameter1": {"value" : 5}}` <p> **Tür**: bool <p> **Bildirim**:`"parameters": {"parameter1": {"type": "bool"}}` <p> **Belirtimi**:`"parameters": {"parameter1": { "value": true }}` <p> **Tür**: dizi <p> **Bildirim**:`"parameters": {"parameter1": {"type": "array"}}` <p> **Belirtimi**:`"parameters": {"parameter1": { "value": [ array-of-values ]}}` <p> **Tür**: nesnesi <p> **Bildirim**:`"parameters": {"parameter1": {"type": "object"}}` <p> **Belirtimi**:`"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Tür**: secureobject <p> **Bildirim**:`"parameters": {"parameter1": {"type": "object"}}` <p> **Belirtimi**:`"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Not:** hello `securestring` ve `secureobject` türleri alınmadı içinde `GET` işlemleri. Tüm parolalar, anahtarlar ve gizli anahtarları bu türünü kullanmanız gerekir.|  
|defaultValue|Hayır|Hiçbir değer hello kaynak oluşturulan hello aynı anda belirtildiğinde hello hello parametresinin varsayılan değeri belirtir.|  
|allowedValues|Hayır|Merhaba parametresi için izin verilen değerler dizisini belirtir.|  
|Meta veriler|Hayır|Okunabilir açıklama veya Visual Studio veya diğer araçları tarafından kullanılan tasarım zamanı verileri gibi hello parametresi ile ilgili ayrıntılı bilgileri belirtir.|  
  
Bu örnek, bir parametre hello gövde bölümünü bir eylem nasıl kullanabileceğiniz gösterilmektedir:  
  
```json
"body" :
{
  "property1": "@parameters('parameter1')"
}
```

 Parametreleri çıktılarında de kullanılabilir.  
  
## <a name="triggers-and-actions"></a>Tetikleyiciler ve eylemler  

Tetikleyiciler ve Eylemler katılabilir hello çağrıları iş akışı yürütme belirtin. Bu bölümde hakkında daha fazla ayrıntı için bkz: [iş akışı eylemleri ve Tetikleyicileri](logic-apps-workflow-actions-triggers.md).
  
## <a name="outputs"></a>Çıkışları  

Çıkış çalıştıran bir iş akışından döndürülebilecek bilgilerini belirtin. Örneğin, bir özel durum ya da her çalıştırmak için tootrack istediğiniz değeri varsa, hello verilerde çıkışları çalıştırmak içerebilir. Merhaba veri Merhaba Yönetimi REST API'si çalıştıran ve bu çalıştırmada hello Azure portal için hello yönetim kullanıcı Arabirimi görüntülenir. Panoları oluşturmak için de bu çıktılar tooother dış sistemler Powerbı gibi akabilir. Çıkış olan *değil* toorespond tooincoming istekleri hizmeti REST API'si hello üzerinde kullanılır. Hello kullanarak toorespond tooan gelen isteği `response` eylem türü örnek aşağıda verilmiştir:
  
```json
"outputs": {  
  "key1": {  
    "value": "value1",  
    "type" : "<type-of-value>"  
  }  
} 
```

|Öğe adı|Gerekli|Açıklama|  
|------------------|--------------|-----------------|  
|key1|Evet|Merhaba Çıktı Hello anahtar tanımlayıcısını belirtir. Değiştir **key1** toouse tooidentify hello çıkış istediğiniz bir adla.|  
|değer|Evet|Merhaba Çıktı Hello değerini belirtir.|  
|type|Evet|Belirtilen hello değeri Hello türünü belirtir. Olası değerler türleri şunlardır: <ul><li>`string`</li><li>`securestring`</li><li>`int`</li><li>`bool`</li><li>`array`</li><li>`object`</li></ul>|
  
## <a name="expressions"></a>İfadeler  

JSON değerler hello tanımında değişmez değer olabilir veya hello tanımı kullanıldığında değerlendirilen bir ifade olabilir. Örneğin:  
  
```json
"name": "value"
```

 or  
  
```json
"name": "@parameters('password') "
```

> [!NOTE]
> Bazı ifadeleri değerlerini hello hello yürütme başlangıcında varolmayabilir çalışma zamanı eylemlerine alırlar. Kullanabileceğiniz **işlevleri** toohelp bu değerlerden bazıları alın.  
  
İfadeler bir JSON dizesi değerindeki herhangi bir yerde görünür ve her zaman başka bir JSON değeri neden. Bir JSON değeri belirlendiği toobe bir ifade kaldığında hello ifadesinin hello gövdesi at işareti için hello kaldırarak ayıklanan (@). Sabit değerli bir dize ile başlayan gerekliyse, @, dize kullanarak kaçış uygulanmalıdır@. Merhaba aşağıdaki ifadeler nasıl değerlendirilir örnekler.  
  
|JSON değeri|Sonuç|  
|----------------|------------|  
|"parametreleri"|Merhaba karakterleri 'parameters' döndürülür.|  
|"parametreleri [1]"|Merhaba karakterleri 'parametreleri [1]' döndürülür.|  
|"@@"|İçeren bir 1 karakter dizesi ' @' döndürülür.|  
|" @"|İçeren bir 2 karakter dizesi ' @' döndürülür.|  
  
İle *dize ilişkilendirme*, ifadeler burada ifadeleri sarılır içinde dizeleri içinde de görüntülenebilir `@{ ... }`. Örneğin: <p>`"name" : "First Name: @{parameters('firstName')} Last Name: @{parameters('lastName')}"`

Merhaba sonucu olan her zaman bu özellik benzer toohello olmasını sağlayan bir dize `concat` işlevi. Tanımladığınız varsayalım `myNumber` olarak `42` ve `myString` olarak `sampleString`:  
  
|JSON değeri|Sonuç|  
|----------------|------------|  
|"@parameters('myString')"|Döndürür `sampleString` dize olarak.|  
|"@{parameters('myString')}"|Döndürür `sampleString` dize olarak.|  
|"@parameters('myNumber')"|Döndürür `42` olarak bir *numarası*.|  
|"@{parameters('myNumber')}"|Döndürür `42` olarak bir *dize*.|  
|"Yanıt: @{parameters('myNumber')}"|Döndürür hello dize `Answer is: 42`.|  
|"@concat(' Yanıt: ', string(parameters('myNumber')))"|Merhaba dize verir`Answer is: 42`|  
|"Yanıt: @@ {parameters('myNumber')}"|Döndürür hello dize `Answer is: @{parameters('myNumber')}`.|  
  
## <a name="operators"></a>İşleçler  

İşleçler ifadeler veya işlevler içinde kullanabileceğiniz hello karakterlerdir. 
  
|işleci|Açıklama|  
|--------------|-----------------|  
|.|Merhaba dot işleci bir nesnenin tooreference özelliği sağlar|  
|?|Hello soru işareti işleci, null bir çalışma zamanı hatası olmadan bir nesnenin özelliklerini başvuru sağlar. Örneğin, bu deyim toohandle null kullanabilirsiniz tetiklemek çıkarır: <p>`@coalesce(trigger().outputs?.body?.property1, 'my default value')`|  
|'|Merhaba tek tırnak işareti hello tek yolu toowrap dize hazır olur. Bu noktalama hello tüm ifade sarmalar hello JSON teklifle çakıştığından, çift tırnak içine ifadeleri kullanamazsınız.|  
|[]|Merhaba köşeli kullanılan tooget belirli bir dizine sahip bir dizi arasında bir değer olabilir. Başarılı bir eylem varsa, örneğin, `range(0,10)`toohello içinde `forEach` işlevi, bu işlevi tooget öğeleri dizisi kullanabilirsiniz:  <p>`myArray[item()]`|  
  
## <a name="functions"></a>İşlevler  

Ayrıca, ifadeler işlevlerinde çağırabilirsiniz. Merhaba aşağıdaki tabloda kullanılabilir hello işlevleri bir ifadede gösterilmektedir.  
  
|ifade|Değerlendirme|  
|----------------|----------------|  
|"@function('Hello')"|Çağrıları hello değişmez değer dize Hello hello tanımıyla hello birinci parametre olarak işlevin üyesi hello.|  
|"@function('Bu harika!')"|Merhaba değişmez değer dize ile Merhaba tanımının 'Cool kadar!' hello işlevi üye çağırır Merhaba ilk parametre olarak|  
|"@function() .prop1"|Merhaba hello prop1 özelliğinin değerini döndürür hello `myfunction` hello tanımı üyesi.|  
|"@function('Hello') .prop1"|Çağrıları hello değişmez değer dize 'Hello' hello tanımıyla işlevi üyesi hello ilk parametre ve döndürür hello prop1 hello nesnesinin özelliği olarak hello.|  
|"@function(parameters('Hello'))"|Merhaba Hello parametre değerlendirir ve hello değeri toofunction geçirir|  
  
### <a name="referencing-functions"></a>İşlevler başvurma  

Bu işlevler tooreference çıkışları diğer eylemlerine hello mantıksal uygulama veya hello mantıksal uygulama oluşturulduğunda geçirilen değerleri kullanabilirsiniz. Örneğin, bir adım toouse hello veri başvurabilir, başka bir.  
  
|İşlev adı|Açıklama|  
|-------------------|-----------------|  
|Parametreleri|Merhaba tanımında tanımlanan bir parametre değeri döndürür. <p>`parameters('password')` <p> **Numaralı parametre**: 1 <p> **Ad**: parametre <p> **Açıklama**: gerekli. değerleri istediğiniz hello parametresinin Hello adı.|  
|Eylem|Bir ifade tooderive diğer JSON ad ve değer çiftleri veya hello geçerli çalışma zamanı eylemin hello çıkış değerini sağlar. Aşağıdaki örneğine hello içinde propertyPath tarafından temsil edilen hello özellik isteğe bağlıdır. PropertyPath belirtilmezse, hello başvuru toohello tüm eylem nesnesidir. Bu işlev yalnızca içinde kullanılabilir-bir eylem koşullarını kadar. <p>`action().outputs.body.propertyPath`|  
|Eylemler|Bir ifade tooderive diğer JSON ad ve değer çiftleri veya hello çalışma zamanı eylemin hello çıkış değerini sağlar. Bu ifadeler, açıkça bir eylem başka bir eyleme dayanan bildirin. Aşağıdaki örneğine hello içinde propertyPath tarafından temsil edilen hello özellik isteğe bağlıdır. PropertyPath belirtilmezse, hello başvuru toohello tüm eylem nesnesidir. Ya da bu öğe kullanabilirsiniz veya hello koşulları öğesi toospecify bağımlılıkları, ancak Merhaba toouse hem gerekmez aynı bağımlı kaynak. <p>`actions('myAction').outputs.body.propertyPath` <p> **Numaralı parametre**: 1 <p> **Ad**: eylem adı <p> **Açıklama**: gerekli. değerleri istediğiniz hello eylemin Hello adı. <p> Merhaba eylem nesnesindeki kullanılabilir özellikleri şunlardır: <ul><li>`name`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Merhaba bkz [Rest API](http://go.microsoft.com/fwlink/p/?LinkID=850646) bu özellikleri hakkında ayrıntılı bilgi için.|
|Tetikleyici|Bir ifade tooderive diğer JSON ad ve değer çiftleri veya hello çalışma zamanı tetikleyici hello çıktısını değerini sağlar. Aşağıdaki örneğine hello içinde propertyPath tarafından temsil edilen hello özellik isteğe bağlıdır. PropertyPath belirtilmezse, hello başvuru toohello tüm tetikleyici nesnesidir. <p>`trigger().outputs.body.propertyPath` <p>İçinde bir tetikleyicinin girişleri kullanıldığında hello işlevi hello önceki yürütme hello çıkışları döndürür. Ancak, bir tetikleyici koşul içinde kullanıldığında, hello `trigger` işlevi hello geçerli yürütme hello çıkışları döndürür. <p> Merhaba tetikleyici nesnesindeki kullanılabilir özellikleri şunlardır: <ul><li>`name`</li><li>`scheduledTime`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Merhaba bkz [Rest API](http://go.microsoft.com/fwlink/p/?LinkID=850644) bu özellikleri hakkında ayrıntılı bilgi için.|
|actionOutputs|Bu işlev için toplu özelliktir`actions('actionName').outputs` <p> **Numaralı parametre**: 1 <p> **Ad**: eylem adı <p> **Açıklama**: gerekli. değerleri istediğiniz hello eylemin Hello adı.|  
|actionBody ve gövde|Bu işlevler için kestirme olan`actions('actionName').outputs.body` <p> **Numaralı parametre**: 1 <p> **Ad**: eylem adı <p> **Açıklama**: gerekli. değerleri istediğiniz hello eylemin Hello adı.|  
|triggerOutputs|Bu işlev için toplu özelliktir`trigger().outputs`|  
|triggerBody|Bu işlev için toplu özelliktir`trigger().outputs.body`|  
|Öğesi|İçinde bir yinelenen eylemi kullanıldığında, bu işlev hello eyleminin bu yineleme için hello dizisindeki olduğu hello öğeyi döndürür. Örneğin, her öğe için bir dizi iletileri çalıştıran bir eylem varsa, bu söz dizimini kullanabilirsiniz: <p>`"input1" : "@item().subject"`| 
  
### <a name="collection-functions"></a>Toplama işlevleri  

Bu işlevler koleksiyonlar çalışır ve genellikle tooArrays, dizeleri ve bazen sözlükler uygulayın.  
  
|İşlev adı|Açıklama|  
|-------------------|-----------------|  
|içerir|Dize alt dizeyi içeren veya sözlük bir anahtar, listesi içeriyorsa true döndürür değeri içeriyor. Örneğin, bu işlevi döndürür `true`: <p>`contains('abacaba','aca')` <p> **Numaralı parametre**: 1 <p> **Ad**: koleksiyonundaki <p> **Açıklama**: gerekli. Merhaba koleksiyonu toosearch içinde. <p> **Numaralı parametre**: 2 <p> **Ad**: Bul nesnesi <p> **Açıklama**: gerekli. Nesne toofind hello içinde hello **koleksiyonundaki**.|  
|uzunluğu|Bir dizi veya dize öğe sayısını döndürür hello. Örneğin, bu işlevi döndürür `3`:  <p>`length('abc')` <p> **Numaralı parametre**: 1 <p> **Ad**: koleksiyonu <p> **Açıklama**: gerekli. hangi tooget hello uzunluğu için Hello koleksiyonu.|  
|boş|Nesne, dizi veya dize boşsa, true döndürür. Örneğin, bu işlevi döndürür `true`: <p>`empty('')` <p> **Numaralı parametre**: 1 <p> **Ad**: koleksiyonu <p> **Açıklama**: gerekli. boşsa koleksiyonu toocheck hello.|  
|kesişim|Tek bir dizi veya dizi ya da geçirilen nesneleri arasında ortak öğeler olan nesneyi döndürür. Örneğin, bu işlevi döndürür `[1, 2]`: <p>`intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])` <p>Merhaba parametreleri hello işlevi için bir dizi nesneyi veya bir dizi diziler (değil her ikisinin bir karışımıyla) ya da olabilir. Merhaba ile iki nesne varsa aynı, hello son nesne bu adı taşıyan hello son nesnesinde görünen adı. <p> **Numaralı parametre**: 1...*n* <p> **Ad**: koleksiyonu*n* <p> **Açıklama**: gerekli. Merhaba koleksiyonları tooevaluate. Bir nesne hello sonuç tooappear geçirilen tüm koleksiyonlar olması gerekir.|  
|birleşim|Tek bir dizi veya nesne toothis işlevi dizi veya nesne geçirilen tüm hello öğeleri döndürür. Örneğin, bu işlevi döndürür `[1, 2, 3, 10, 101]`: <p>`union([1, 2, 3], [101, 2, 1, 10])` <p>Merhaba parametreleri hello işlevi için bir dizi nesneyi veya bir dizi diziler (olmayan bir karışımını bunların) ya da olabilir. Hello son çıktıda hello aynı ad ile iki nesne varsa, bu adı taşıyan hello son nesne hello son nesnesinde görüntülenir. <p> **Numaralı parametre**: 1...*n* <p> **Ad**: koleksiyonu*n* <p> **Açıklama**: gerekli. Merhaba koleksiyonları tooevaluate. Merhaba koleksiyonları hiçbirinde görünen bir nesnenin hello sonucunda da görüntülenir.|  
|ilk|Hello dizinin ilk öğesi döndürür hello veya dize geçirildi. Örneğin, bu işlevi döndürür `0`: <p>`first([0,2,3])` <p> **Numaralı parametre**: 1 <p> **Ad**: koleksiyonu <p> **Açıklama**: gerekli. Merhaba koleksiyonu tootake hello ilk nesnesinden.|  
|Son|Hello dizide son öğe döndürür hello veya dize geçirildi. Örneğin, bu işlevi döndürür `3`: <p>`last('0123')` <p> **Numaralı parametre**: 1 <p> **Ad**: koleksiyonu <p> **Açıklama**: gerekli. Merhaba koleksiyonu tootake hello son nesnesinden.|  
|Al|Döndürür hello ilk **sayısı** hello dizisi veya dize öğelerinden geçirildi. Örneğin, bu işlevi döndürür `[1, 2]`:  <p>`take([1, 2, 3, 4], 2)` <p> **Numaralı parametre**: 1 <p> **Ad**: koleksiyonu <p> **Açıklama**: gerekli. Merhaba koleksiyondan tootake hello ilk nerede **sayısı** nesneleri. <p> **Numaralı parametre**: 2 <p> **Ad**: sayısı <p> **Açıklama**: gerekli. Merhaba hello gelen nesneleri tootake sayısı **koleksiyonu**. Pozitif bir tamsayı olmalıdır.|  
|Atla|Döndürür hello dizinden başlayarak hello dizideki öğeler **sayısı**. Örneğin, bu işlevi döndürür `[3, 4]`: <p>`skip([1, 2 ,3 ,4], 2)` <p> **Numaralı parametre**: 1 <p> **Ad**: koleksiyonu <p> **Açıklama**: gerekli. Koleksiyon tooskip hello ilk hello **sayısı** nesnelerin. <p> **Numaralı parametre**: 2 <p> **Ad**: sayısı <p> **Açıklama**: gerekli. Merhaba Merhaba öne nesneleri tooremove sayısı **koleksiyonu**. Pozitif bir tamsayı olmalıdır.|  
|join|Örneğin bu döndürür bir sınırlayıcısıyla birleştirilmiş bir dizinin her bir öğesiyle bir dize döndürür `"1,2,3,4"`:<br /><br /> `join([1, 2, 3, 4], ',')`<br /><br /> **Numaralı parametre**: 1<br /><br /> **Ad**: koleksiyonu<br /><br /> **Açıklama**: gerekli. Merhaba koleksiyonu toojoin öğelerinden.<br /><br /> **Numaralı parametre**: 2<br /><br /> **Ad**: sınırlayıcı<br /><br /> **Açıklama**: gerekli. Merhaba dize toodelimit öğeleri.|  
  
### <a name="string-functions"></a>Dize işlevleri

İşlevler yalnızca aşağıdaki hello toostrings uygulayın. Dizeleri bazı toplama işlevleri de kullanabilirsiniz.  
  
|İşlev adı|Açıklama|  
|-------------------|-----------------|  
|concat|Dizeleri herhangi bir sayıda birlikte birleştirir. Örneğin, 1 parametresi ise `p1`, bu işlevi döndürür `somevalue-p1-somevalue`: <p>`concat('somevalue-',parameters('parameter1'),'-somevalue')` <p> **Numaralı parametre**: 1...*n* <p> **Ad**: dize*n* <p> **Açıklama**: gerekli. tek bir dize halinde Hello dizeleri toocombine.|  
|substring|Bir dizeden karakterleri kümesini döndürür. Örneğin, bu işlevi döndürür `abc`: <p>`substring('somevalue-abc-somevalue',10,3)` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba dize hangi hello substring alınır. <p> **Numaralı parametre**: 2 <p> **Ad**: Başlangıç dizini <p> **Açıklama**: gerekli. Merhaba substring parametresi 1 başladığı, başlangıç dizini. <p> **Numaralı parametre**: 3 <p> **Ad**: uzunluğu <p> **Açıklama**: gerekli. Merhaba dizenin Hello uzunluğu.|  
|Değiştir|Bir dizeyi belirli bir dizeyle değiştirir. Örneğin, bu işlevi döndürür `hello new string`: <p>`replace('hello old string', 'old', 'new')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. parametresi 2 için arama ve parametre 2 parametresi 1 bulunduğunda 3 parametreyle güncelleştirilen hello dizesi. <p> **Numaralı parametre**: 2 <p> **Ad**: eski dizesi <p> **Açıklama**: gerekli. Merhaba dize tooreplace parametresi 1 parametresinde bir eşleşme bulunduğunda 3 ile <p> **Numaralı parametre**: 3 <p> **Ad**: yeni bir dize <p> **Açıklama**: gerekli. Merhaba bir dize parametresi 2 kullanılan tooreplace hello dizesinde 1 parametresinde bir eşleşme bulunduğunda.|  
|GUID|Bu işlev, genel olarak benzersiz bir dize (GUID) oluşturur. Örneğin, bu işlev bu GUID oluşturabilirsiniz:`c2ecc88d-88c8-4096-912c-d6f2e2b138ce` <p>`guid()` <p> **Numaralı parametre**: 1 <p> **Ad**: biçimi <p> **Açıklama**: isteğe bağlı. Gösteren bir tek biçim belirticisi [nasıl tooformat hello bu GUID değeri](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx). Merhaba format parametresi "N", "D", "B", "P" veya "X" olabilir. Biçim sağlanmazsa, "D" kullanılır.|  
|toLower|Bir dize toolowercase dönüştürür. Örneğin, bu işlevi döndürür `two by two is four`: <p>`toLower('Two by Two is Four')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba dize tooconvert toolower büyük. Merhaba karakter dizesi döndürdü hello değiştirmeden, hello dizedeki karakter küçük eşdeğeri yoksa dahil edilir.|  
|toUpper|Bir dize toouppercase dönüştürür. Örneğin, bu işlevi döndürür `TWO BY TWO IS FOUR`: <p>`toUpper('Two by Two is Four')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba dize tooconvert tooupper büyük. Merhaba karakter dizesi döndürdü hello değiştirmeden, hello dizedeki karakter büyük bir eşdeğeri yoksa dahil edilir.|  
|IndexOf|Bir dize çalışması içinde bir değerle Hello dizini insensitively bulun. Örneğin, bu işlevi döndürür `7`: <p>`indexof('hello, world.', 'world')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba değer içerebilir hello dizesi. <p> **Numaralı parametre**: 2 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba değeri toosearch başlangıç dizini.|  
|lastIndexOf|Bir dize çalışması içinde bir değerle Hello son dizini insensitively bulun. Örneğin, bu işlevi döndürür `3`: <p>`lastindexof('foofoo', 'foo')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba değer içerebilir hello dizesi. <p> **Numaralı parametre**: 2 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba değeri toosearch başlangıç dizini.|  
|startswith|Merhaba dize değeri durumuyla insensitively başlayıp başlamadığını denetler. Örneğin, bu işlevi döndürür `true`: <p>`startswith('hello, world', 'hello')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba değer içerebilir hello dizesi. <p> **Numaralı parametre**: 2 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba değer hello dizesi ile başlayabilir.|  
|endswith|Merhaba dize değeri durumuyla insensitively bitip bitmediğini denetler. Örneğin, bu işlevi döndürür `true`: <p>`endswith('hello, world', 'world')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba değer içerebilir hello dizesi. <p> **Numaralı parametre**: 2 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba değer hello dizesi ile bitebilir.|  
|split|Ayırıcı kullanarak hello dize böler. Örneğin, bu işlevi döndürür `["a", "b", "c"]`: <p>`split('a;b;c',';')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Bölünen hello dizesi. <p> **Numaralı parametre**: 2 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba ayırıcı.|  
  
### <a name="logical-functions"></a>Mantıksal işlevleri  

Bu işlevler içinde koşullar yararlıdır ve kullanılan tooevaluate mantığı herhangi bir türde olabilir.  
  
|İşlev adı|Açıklama|  
|-------------------|-----------------|  
|eşittir|İki değer eşitse true değerini döndürür. Örneğin, parametre1 someValue ise, bu işlev, döndürür `true`: <p>`equals(parameters('parameter1'), 'someValue')` <p> **Numaralı parametre**: 1 <p> **Ad**: 1 nesne <p> **Açıklama**: gerekli. Nesne toocompare çok hello**nesne 2**. <p> **Numaralı parametre**: 2 <p> **Ad**: 2 nesnesi <p> **Açıklama**: gerekli. Nesne toocompare çok hello**nesne 1**.|  
|daha az|Merhaba ilk bağımsız değişken hello değerinden ikinci ise true değeri döndürür. Not, değerler yalnızca türü tamsayı, kayan noktalı sayı veya dize olabilir. Örneğin, bu işlevi döndürür `true`: <p>`less(10,100)` <p> **Numaralı parametre**: 1 <p> **Ad**: 1 nesne <p> **Açıklama**: gerekli. Bu nesne toocheck hello değerinden **nesne 2**. <p> **Numaralı parametre**: 2 <p> **Ad**: 2 nesnesi <p> **Açıklama**: gerekli. ' den büyükse, nesne toocheck hello **nesne 1**.|  
|lessOrEquals|Merhaba ilk bağımsız değişkeni ise true değeri döndürür küçüktür veya toohello ikinci eşit. Not, değerler yalnızca türü tamsayı, kayan noktalı sayı veya dize olabilir. Örneğin, bu işlevi döndürür `true`: <p>`lessOrEquals(10,10)` <p> **Numaralı parametre**: 1 <p> **Ad**: 1 nesne <p> **Açıklama**: gerekli. çok eşit veya daha az ise, nesne toocheck hello**nesne 2**. <p> **Numaralı parametre**: 2 <p> **Ad**: 2 nesnesi <p> **Açıklama**: gerekli. çok eşit veya daha büyükse, nesne toocheck hello**nesne 1**.|  
|büyük|Merhaba ilk bağımsız değişken ikinci hello büyükse, true döndürür. Not, değerler yalnızca türü tamsayı, kayan noktalı sayı veya dize olabilir. Örneğin, bu işlevi döndürür `false`:  <p>`greater(10,10)` <p> **Numaralı parametre**: 1 <p> **Ad**: 1 nesne <p> **Açıklama**: gerekli. ' den büyükse, nesne toocheck hello **nesne 2**. <p> **Numaralı parametre**: 2 <p> **Ad**: 2 nesnesi <p> **Açıklama**: gerekli. Bu nesne toocheck hello değerinden **nesne 1**.|  
|greaterOrEquals|Merhaba ilk bağımsız değişkeni sıfırdan büyük veya eşit toohello ikinci ise true değerini döndürür. Not, değerler yalnızca türü tamsayı, kayan noktalı sayı veya dize olabilir. Örneğin, bu işlevi döndürür `false`: <p>`greaterOrEquals(10,100)` <p> **Numaralı parametre**: 1 <p> **Ad**: 1 nesne <p> **Açıklama**: gerekli. çok eşit veya daha büyükse, nesne toocheck hello**nesne 2**. <p> **Numaralı parametre**: 2 <p> **Ad**: 2 nesnesi <p> **Açıklama**: gerekli. küçük veya buna eşit olması durumunda nesne toocheck hello çok**nesne 1**.|  
|ve|Parametrelerinin her ikisini de doğruysa, true döndürür. Her iki değişken toobe Boole değerlerini gerekir. Örneğin, bu işlevi döndürür `false`: <p>`and(greater(1,10),equals(0,0))` <p> **Numaralı parametre**: 1 <p> **Ad**: Boolean 1 <p> **Açıklama**: gerekli. Merhaba olmalıdır ilk bağımsız değişken `true`. <p> **Numaralı parametre**: 2 <p> **Ad**: Boolean 2 <p> **Açıklama**: gerekli. Merhaba ikinci bağımsız değişkeni olmalıdır `true`.|  
|or|Her iki parametre true olduğunda true değerini döndürür. Her iki değişken toobe Boole değerlerini gerekir. Örneğin, bu işlevi döndürür `true`: <p>`or(greater(1,10),equals(0,0))` <p> **Numaralı parametre**: 1 <p> **Ad**: Boolean 1 <p> **Açıklama**: gerekli. Merhaba olabilir ilk bağımsız değişken `true`. <p> **Numaralı parametre**: 2 <p> **Ad**: Boolean 2 <p> **Açıklama**: gerekli. Merhaba ikinci bağımsız değişken olabilir `true`.|  
|değil|Merhaba parametreleri ise true döndürür `false`. Her iki değişken toobe Boole değerlerini gerekir. Örneğin, bu işlevi döndürür `true`: <p>`not(contains('200 Success','Fail'))` <p> **Numaralı parametre**: 1 <p> **Ad**: Boolean <p> **Açıklama**: hello parametreleri ise true değerini döndürür `false`. Her iki değişken toobe Boole değerlerini gerekir. Bu işlev, döndürür `true`:`not(contains('200 Success','Fail'))`|  
|Eğer|Olup hello ifade ile sonuçlandı üzerinde temel belirtilen değeri döndüren `true` veya `false`.  Örneğin, bu işlevi döndürür `"yes"`: <p>`if(equals(1, 1), 'yes', 'no')` <p> **Numaralı parametre**: 1 <p> **Ad**: ifade <p> **Açıklama**: gerekli. Hangi değer hello ifadesi belirleyen bir boolean değeri döndürmelidir. <p> **Numaralı parametre**: 2 <p> **Ad**: True <p> **Açıklama**: gerekli. Merhaba ifade ise, değer tooreturn hello `true`. <p> **Numaralı parametre**: 3 <p> **Ad**: yanlış <p> **Açıklama**: gerekli. Merhaba ifade ise, değer tooreturn hello `false`.|  
  
### <a name="conversion-functions"></a>Dönüşüm işlevleri  

Bu işlevlerin her hello hello dil içindeki yerel türler arasında kullanılan tooconvert şunlardır:  
  
- Dize  
  
- tamsayı  
  
- Kayan nokta  
  
- Boole değeri  
  
- Diziler  
  
- Sözlük  

-   Formlar  
  
|İşlev adı|Açıklama|  
|-------------------|-----------------|  
|Int|Merhaba parametresi tooan tamsayı dönüştürün. Örneğin, bu işlev bir dize yerine bir sayı olarak 100 döndürür: <p>`int('100')` <p> **Numaralı parametre**: 1 <p> **Ad**: değer <p> **Açıklama**: gerekli. Dönüştürülen tooan tamsayıdır hello değeri.|  
|Dize|Merhaba parametre tooa dizesi dönüştürün. Örneğin, bu işlevi döndürür `'10'`: <p>`string(10)` <p>Ayrıca, bir nesne tooa dize dönüştürebilirsiniz. Örneğin, hello `myPar` parametredir bir özelliği olan bir nesne `abc : xyz`, bu işlevi döndürür sonra `{"abc" : "xyz"}`: <p>`string(parameters('myPar'))` <p> **Numaralı parametre**: 1 <p> **Ad**: değer <p> **Açıklama**: gerekli. Merhaba değer dönüştürülmüş tooa dize.|  
|JSON|Merhaba tooa JSON türünü bir parametre dönüştürme ve, ters hello olduğundan `string()`. Örneğin, bu işlevi döndürür `[1,2,3]` bir dize yerine bir dizi olarak: <p>`json('[1,2,3]')` <p>Benzer şekilde, bir dize tooan nesnesi dönüştürebilirsiniz. Örneğin, bu işlevi döndürür `{ "abc" : "xyz" }`: <p>`json('{"abc" : "xyz"}')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba dize dönüştürülmüş tooa yerel tür değeri. <p>Merhaba `json()` işlevi çok giriş XML destekler. Örneğin, hello parametre değeri: <p>`<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>` <p>Dönüştürülen toothis JSON değil: <p>`{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|Kayan nokta|Merhaba parametre bağımsız değişkeni tooa kayan noktalı sayı dönüştürün. Örneğin, bu işlevi döndürür `10.333`: <p>`float('10.333')` <p> **Numaralı parametre**: 1 <p> **Ad**: değer <p> **Açıklama**: gerekli. Merhaba değer dönüştürülmüş tooa kayan noktalı sayı.|  
|bool|Merhaba parametresi tooa Boolean dönüştürün. Örneğin, bu işlevi döndürür `false`: <p>`bool(0)` <p> **Numaralı parametre**: 1 <p> **Ad**: değer <p> **Açıklama**: gerekli. Merhaba dönüştürülmüş tooa değeri boolean.|  
|birleşim|Geçirilen hello bağımsız Hello ilk null olmayan nesne döndürür. **Not**: boş bir dize null değil. Örneğin, 1 ve 2 parametreleri tanımlanmazsa, bu işlev, döndürür `fallback`:  <p>`coalesce(parameters('parameter1'), parameters('parameter2') ,'fallback')` <p> **Numaralı parametre**: 1...*n* <p> **Ad**: nesnesi*n* <p> **Açıklama**: gerekli. Merhaba nesneleri toocheck, null.|  
|Base64|Base64 hello giriş dize gösterimini döndürür hello. Örneğin, bu işlevi döndürür `c29tZSBzdHJpbmc=`: <p>`base64('some string')` <p> **Numaralı parametre**: 1 <p> **Ad**: Dize 1 <p> **Açıklama**: gerekli. dize tooencode base64 gösterimine hello.|  
|base64ToBinary|Bir base64 kodlu dize ikili bir gösterimini döndürür. Örneğin, bu işlev hello ikili gösterimini döndürür `some string`: <p>`base64ToBinary('c29tZSBzdHJpbmc=')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba Base64 ile kodlanmış dizesi.|  
|base64ToString|Kodlanmış based64 dize dize gösterimini döndürür. Örneğin, bu işlevi döndürür `some string`: <p>`base64ToString('c29tZSBzdHJpbmc=')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba Base64 ile kodlanmış dizesi.|  
|İkili|Değer ikili bir gösterimini döndürür.  Örneğin, bu işlev bir ikili biçimi döndürür `some string`: <p>`binary('some string')` <p> **Numaralı parametre**: 1 <p> **Ad**: değer <p> **Açıklama**: gerekli. Dönüştürülen toobinary hello değer.|  
|dataUriToBinary|Bir ikili veri URI'si gösterimini döndürür. Örneğin, bu işlev hello ikili gösterimini döndürür `some string`: <p>`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba veri URI tooconvert toobinary gösterimi.|  
|dataUriToString|Bir veri URI dize gösterimini döndürür. Örneğin, bu işlevi döndürür `some string`: <p>`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize<p> **Açıklama**: gerekli. Merhaba veri URI tooconvert tooString gösterimi.|  
|dataUri|Bir veri URI değeri döndürür. Örneğin, bu işlev, bu verileri URI döndürür `text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=`: <p>`dataUri('some string')` <p> **Numaralı parametre**: 1<p> **Ad**: değer<p> **Açıklama**: gerekli. Merhaba değeri tooconvert toodata URI.|  
|decodeBase64|Bir giriş based64 dize dize gösterimini döndürür. Örneğin, bu işlevi döndürür `some string`: <p>`decodeBase64('c29tZSBzdHJpbmc=')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: bir giriş based64 dize dize gösterimini döndürür.|  
|Encodeurıcomponent|Geçirilen URL çıkışları hello dizesi. Örneğin, bu işlevi döndürür `You+Are%3ACool%2FAwesome`: <p>`encodeUriComponent('You Are:Cool/Awesome')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba dize tooescape URL güvenli olmayan karakterler.|  
|Decodeurıcomponent|Geçirilen kaydını URL çıkışları hello dizesi. Örneğin, bu işlevi döndürür `You Are:Cool/Awesome`: <p>`encodeUriComponent('You+Are%3ACool%2FAwesome')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba dize toodecode hello URL güvenli olmayan karakterler.|  
|decodeDataUri|İkili bir giriş verileri URI dize gösterimini döndürür. Örneğin, bu işlev hello ikili gösterimini döndürür `some string`: <p>`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba dataURI toodecode içine bir ikili biçimi.|  
|uriComponent|Bir URI döndürür değerinin gösterimiyle kodlanmış. Örneğin, bu işlevi döndürür `You+Are%3ACool%2FAwesome`: <p>`uriComponent('You Are:Cool/Awesome')` <p> **Numaralı parametre**: 1<p> **Ad**: dize <p> **Açıklama**: gerekli. Merhaba dize toobe kodlanmış URI.|  
|uriComponentToBinary|Bir URI ikili gösterimidir kodlanmış dizesi döndürür. Örneğin, bu işlev bir ikili biçimi döndürür `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Numaralı parametre**: 1 <p> **Ad**: dize<p> **Açıklama**: gerekli. Merhaba URI kodlanmış dizesi.|  
|uriComponentToString|Bir URI dize gösterimini kodlanmış dizesi döndürür. Örneğin, bu işlevi döndürür `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Numaralı parametre**: 1<p> **Ad**: dize<p> **Açıklama**: gerekli. Merhaba URI kodlanmış dizesi.|  
|xml|Merhaba değerinin XML gösterimini döndürür. Örneğin, bu işlev XML tarafından temsil edilen içerik döndürür `'\<name>Alan\</name>'`: <p>`xml('\<name>Alan\</name>')` <p>Merhaba `xml()` işlevi çok giriş JSON nesnesi destekler. Örneğin, parametre hello `{ "abc": "xyz" }` dönüştürülmüş tooXML içerik türüdür:`\<abc>xyz\</abc>` <p> **Numaralı parametre**: 1<p> **Ad**: değer<p> **Açıklama**: gerekli. Merhaba değeri tooconvert tooXML.|  
|XPath|XML düğümlerini hello xpath ifadesi hello xpath ifadesi değerlendiren bir değeri ile eşleşen bir dizi döndürür. <p> **Örnek 1** <p>Merhaba parametresinin değerini varsayın `p1` bu XML dize gösterimi ise: <p>`<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>` <p>Bu kod:`xpath(xml(parameters('p1'), '/lab/robot/name')` <p>döndürür <p>`[ <name>R1</name>, <name>R2</name> ]` <p>Bu kodu: <p>`xpath(xml(parameters('p1'), ' sum(/lab/robot/parts)')` <p>döndürür <p>`13` <p> <p> **Örnek 2** <p>XML içeriği aşağıdaki verilen hello: <p>`<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>` <p>Bu kod:`@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')` <p>veya bu kod: <p>`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')` <p>döndürür <p>`<Location xmlns="http://abc.com">xyz</Location>` <p>Ve bu kodu:`@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')` <p>döndürür <p>``xyz`` <p> **Numaralı parametre**: 1 <p> **Ad**: Xml <p> **Açıklama**: gerekli. Merhaba XML üzerinde hangi tooevaluate hello XPath ifadesi. <p> **Numaralı parametre**: 2 <p> **Ad**: XPath <p> **Açıklama**: gerekli. Merhaba XPath ifadesi tooevaluate.|  
|Dizi|Merhaba parametre tooan dizisine dönüştürür. Örneğin, bu işlevi döndürür `["abc"]`: <p>`array('abc')` <p> **Numaralı parametre**: 1 <p> **Ad**: değer <p> **Açıklama**: gerekli. Dönüştürülen tooan dizisi hello değeri.|
|createArray|Bir dizi hello parametrelerinden oluşturur. Örneğin, bu işlevi döndürür `["a", "c"]`: <p>`createArray('a', 'c')` <p> **Numaralı parametre**: 1...*n* <p> **Ad**: tüm*n* <p> **Açıklama**: gerekli. bir dizi içine Hello değerleri toocombine.|
|triggerFormDataValue|Form verileri veya form kodlu tetikleyici Çıktı Hello anahtar adıyla eşleşen tek bir değer döndürür.  Varsa birden çok işlem hata eşleşir.  Örneğin, hello aşağıdaki döndürür `bar`:`triggerFormDataValue('foo')`<br /><br />**Numaralı parametre**: 1<br /><br />**Ad**: anahtar adı<br /><br />**Açıklama**: gerekli. anahtar adı hello form veri değeri tooreturn Hello.|
|triggerFormDataMultiValues|Form verileri veya form kodlu tetikleyici çıktı hello anahtar adıyla eşleşen değerleri dizisi döndürür.  Örneğin, hello aşağıdaki döndürür `["bar"]`:`triggerFormDataValue('foo')`<br /><br />**Numaralı parametre**: 1<br /><br />**Ad**: anahtar adı<br /><br />**Açıklama**: gerekli. anahtar adı hello form veri değerleri tooreturn Hello.|
|triggerMultipartBody|Döndürür gövdesi bir kısmı için çok bölümlü çıktısında hello tetikleyici hello.<br /><br />**Numaralı parametre**: 1<br /><br />**Ad**: dizin<br /><br />**Açıklama**: gerekli. Merhaba bölümü tooretrieve başlangıç dizini.|
|formDataValue|Form verileri veya form kodlu eylem çıkışı Hello anahtar adıyla eşleşen tek bir değer döndürür.  Varsa birden çok işlem hata eşleşir.  Örneğin, hello aşağıdaki döndürür `bar`:`formDataValue('someAction', 'foo')`<br /><br />**Numaralı parametre**: 1<br /><br />**Ad**: eylem adı<br /><br />**Açıklama**: gerekli. form verileri veya form kodlu yanıt hello eylemin Hello adı.<br /><br />**Numaralı parametre**: 2<br /><br />**Ad**: anahtar adı<br /><br />**Açıklama**: gerekli. anahtar adı hello form veri değeri tooreturn Hello.|
|formDataMultiValues|Form verileri veya form kodlu eylem çıkışı hello anahtar adıyla eşleşen değerleri dizisi döndürür.  Örneğin, hello aşağıdaki döndürür `["bar"]`:`formDataMultiValues('someAction', 'foo')`<br /><br />**Numaralı parametre**: 1<br /><br />**Ad**: eylem adı<br /><br />**Açıklama**: gerekli. form verileri veya form kodlu yanıt hello eylemin Hello adı.<br /><br />**Numaralı parametre**: 2<br /><br />**Ad**: anahtar adı<br /><br />**Açıklama**: gerekli. anahtar adı hello form veri değerleri tooreturn Hello.|
|multipartBody|Gövde bir kısmı için çok bölümlü çıktıda bir eylem döndürür hello.<br /><br />**Numaralı parametre**: 1<br /><br />**Ad**: eylem adı<br /><br />**Açıklama**: gerekli. çok bölümlü bir yanıt hello eylemin Hello adı.<br /><br />**Numaralı parametre**: 2<br /><br />**Ad**: dizin<br /><br />**Açıklama**: gerekli. Merhaba bölümü tooretrieve başlangıç dizini.|

### <a name="math-functions"></a>Matematik işlevleri  

Bu işlevlerin her iki tür numarası için kullanılabilir: **tamsayılar** ve **gezinen**.  
  
|İşlev adı|Açıklama|  
|-------------------|-----------------|  
|Ekleme|Merhaba iki sayı ekleme Hello sonucunu döndürür. Örneğin, bu işlevi döndürür `20.333`: <p>`add(10,10.333)` <p> **Numaralı parametre**: 1 <p> **Ad**: Summand 1 <p> **Açıklama**: gerekli. sayı tooadd çok hello**Summand 2**. <p> **Numaralı parametre**: 2 <p> **Ad**: Summand 2 <p> **Açıklama**: gerekli. sayı tooadd çok hello**Summand 1**.|  
|Sub|İki sayı çıkarılmasıyla Hello sonucunu döndürür. Örneğin, bu işlevi döndürür `-0.333`: <p>`sub(10,10.333)` <p> **Numaralı parametre**: 1 <p> **Ad**: Minuend <p> **Açıklama**: gerekli. Merhaba sayı **Subtrahend** kaldırılır. <p> **Numaralı parametre**: 2 <p> **Ad**: Subtrahend <p> **Açıklama**: gerekli. Merhaba gelen sayı tooremove hello **Minuend**.|  
|mul|Merhaba iki sayının çarparak Hello sonucunu döndürür. Örneğin, bu işlevi döndürür `103.33`: <p>`mul(10,10.333)` <p> **Numaralı parametre**: 1 <p> **Ad**: Multiplicand 1 <p> **Açıklama**: gerekli. sayı toomultiply hello **Multiplicand 2** ile. <p> **Numaralı parametre**: 2 <p> **Ad**: Multiplicand 2 <p> **Açıklama**: gerekli. sayı toomultiply hello **Multiplicand 1** ile.|  
|div|Merhaba iki sayının Hello sonucu döndürür. Örneğin, bu işlevi döndürür `1.0333`: <p>`div(10.333,10)` <p> **Numaralı parametre**: 1 <p> **Ad**: bölünen <p> **Açıklama**: gerekli. sayı toodivide tarafından hello hello **bölen**. <p> **Numaralı parametre**: 2 <p> **Ad**: bölen <p> **Açıklama**: gerekli. Merhaba numara toodivide hello **bölünen** tarafından.|  
|mod|(Modül) hello iki sayı bölen sonra Hello kalanı döndürür. Örneğin, bu işlevi döndürür `2`: <p>`mod(10,4)` <p> **Numaralı parametre**: 1 <p> **Ad**: bölünen <p> **Açıklama**: gerekli. sayı toodivide tarafından hello hello **bölen**. <p> **Numaralı parametre**: 2 <p> **Ad**: bölen <p> **Açıklama**: gerekli. Merhaba numara toodivide hello **bölünen** tarafından. Merhaba ayırmadan sonra hello kalan alınır.|  
|dk|Bu işlevi çağırmak için iki farklı modeli vardır. <p>Burada `min` bir dizi alır ve hello işlevi döndürür `0`: <p>`min([0,1,2])` <p>Alternatif olarak, bu işlev virgülle ayrılmış bir liste değerleri ve ayrıca döndürür sürebilir `0`: <p>`min(0,1,2)` <p> **Not**: tüm değerleri sayı olması gerekir, hello parametresi bir dizi ise sahip hello dizisi tooonly vardır, yani sayı. <p> **Numaralı parametre**: 1 <p> **Ad**: koleksiyon veya değeri <p> **Açıklama**: gerekli. Ya da bir dizi değerleri toofind hello en düşük değer veya kümesinin hello ilk değeri. <p> **Numaralı parametre**: 2...*n* <p> **Ad**: değer*n* <p> **Açıklama**: isteğe bağlı. Merhaba ilk parametre bir değer ise, ardından ek değerler geçirebilir ve hello geçirilen tüm değerlerin minimum döndürülür.|  
|max|Bu işlevi çağırmak için iki farklı modeli vardır. <p>Burada `max` bir dizi alır ve hello işlevi döndürür `2`: <p>`max([0,1,2])` <p>Alternatif olarak, bu işlev virgülle ayrılmış bir liste değerleri ve ayrıca döndürür sürebilir `2`: <p>`max(0,1,2)` <p> **Not**: tüm değerleri sayı olması gerekir, hello parametresi bir dizi ise sahip hello dizisi tooonly vardır, yani sayı. <p> **Numaralı parametre**: 1 <p> **Ad**: koleksiyon veya değeri <p> **Açıklama**: gerekli. Ya da bir dizi değerleri toofind hello en büyük değer veya kümesinin hello ilk değeri. <p> **Numaralı parametre**: 2...*n* <p> **Ad**: değer*n* <p> **Açıklama**: isteğe bağlı. Merhaba ilk parametre bir değer ise, ardından ek değerler geçirebilir ve hello geçirilen tüm değerlerin maksimum döndürülür.|  
|Aralık|Belirli bir numarasından başlayarak dizisi oluşturur. Dizi döndürdü hello hello uzunluğunu tanımlayın. <p>Örneğin, bu işlevi döndürür `[3,4,5,6]`: <p>`range(3,4)` <p> **Numaralı parametre**: 1 <p> **Ad**: Başlangıç dizini <p> **Açıklama**: gerekli. Merhaba hello dizinin ilk tamsayı. <p> **Numaralı parametre**: 2 <p> **Ad**: sayısı <p> **Açıklama**: gerekli. Bu değer hello dizisinde olan hello tamsayılar sayısıdır.|  
|rand|Bir rastgele oluşturur tamsayı hello içinde belirtilen aralığı (yalnızca ilk ucunda dahil). Örneğin, bu işlev ya da döndürebilirsiniz `0` veya '1': <p>`rand(0,2)` <p> **Numaralı parametre**: 1 <p> **Ad**: en az <p> **Açıklama**: gerekli. döndürülebilecek hello en küçük tamsayı. <p> **Numaralı parametre**: 2 <p> **Ad**: en fazla <p> **Açıklama**: gerekli. Bu değer hello sonraki tamsayıya döndürülebilen hello yüksek sonra tamsayıdır.|  
  
### <a name="date-functions"></a>Date işlevleri  
  
|İşlev adı|Açıklama|  
|-------------------|-----------------|  
|UtcNow|Döndürür geçerli zaman damgası örneğin bir dize olarak hello: `2017-03-15T13:27:36Z`: <p>`utcnow()` <p> **Numaralı parametre**: 1 <p> **Ad**: biçimi <p> **Açıklama**: isteğe bağlı. Ya da bir [tek bir biçim belirticisi karakter](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) veya [özel biçim deseni](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) nasıl tooformat hello bu zaman damgası değerini gösterir. Biçim sağlanmazsa, hello ISO 8601 biçiminde ("o") kullanılır.|  
|saniyeEkle|Saniye tooa dize zaman damgası geçirilen tamsayı sayısı ekler. Merhaba saniye sayısı pozitif veya negatif olabilir. Bir biçim belirticisi sağlanmadığı sürece varsayılan olarak, hello ISO 8601 dizesinde biçimlendirin ("o"), sonucudur. Örneğin: `2015-03-15T13:27:00Z`: <p>`addseconds('2015-03-15T13:27:36Z', -36)` <p> **Numaralı parametre**: 1 <p> **Ad**: zaman damgası <p> **Açıklama**: gerekli. Başlangıç saati içeren bir dize. <p> **Numaralı parametre**: 2 <p> **Ad**: saniye <p> **Açıklama**: gerekli. Merhaba saniye tooadd sayısı. Negatif toosubtract saniye olabilir. <p> **Numaralı parametre**: 3 <p> **Ad**: biçimi <p> **Açıklama**: isteğe bağlı. Ya da bir [tek bir biçim belirticisi karakter](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) veya [özel biçim deseni](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) nasıl tooformat hello bu zaman damgası değerini gösterir. Biçim sağlanmazsa, hello ISO 8601 biçiminde ("o") kullanılır.|  
|AddMinutes|Dakika tooa dize zaman damgası geçirilen tamsayı sayısı ekler. Merhaba dakika sayısı pozitif veya negatif olabilir. Bir biçim belirticisi sağlanmadığı sürece varsayılan olarak, hello ISO 8601 dizesinde biçimlendirin ("o"), sonucudur. Örneğin: `2015-03-15T14:00:36Z`: <p>`addminutes('2015-03-15T13:27:36Z', 33)` <p> **Numaralı parametre**: 1 <p> **Ad**: zaman damgası <p> **Açıklama**: gerekli. Başlangıç saati içeren bir dize. <p> **Numaralı parametre**: 2 <p> **Ad**: dakika <p> **Açıklama**: gerekli. dakika tooadd Hello sayısı. Negatif toosubtract dakika olabilir. <p> **Numaralı parametre**: 3 <p> **Ad**: biçimi <p> **Açıklama**: isteğe bağlı. Ya da bir [tek bir biçim belirticisi karakter](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) veya [özel biçim deseni](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) nasıl tooformat hello bu zaman damgası değerini gösterir. Biçim sağlanmazsa, hello ISO 8601 biçiminde ("o") kullanılır.|  
|addhours|Saat tooa dize zaman damgası geçirilen tamsayı sayısı ekler. Merhaba kaç saat olumlu veya olumsuz olabilir. Bir biçim belirticisi sağlanmadığı sürece varsayılan olarak, hello ISO 8601 dizesinde biçimlendirin ("o"), sonucudur. Örneğin: `2015-03-16T01:27:36Z`: <p>`addhours('2015-03-15T13:27:36Z', 12)` <p> **Numaralı parametre**: 1 <p> **Ad**: zaman damgası <p> **Açıklama**: gerekli. Başlangıç saati içeren bir dize. <p> **Numaralı parametre**: 2 <p> **Ad**: saat <p> **Açıklama**: gerekli. saat tooadd Hello sayısı. Negatif toosubtract saat olabilir. <p> **Numaralı parametre**: 3 <p> **Ad**: biçimi <p> **Açıklama**: isteğe bağlı. Ya da bir [tek bir biçim belirticisi karakter](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) veya [özel biçim deseni](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) nasıl tooformat hello bu zaman damgası değerini gösterir. Biçim sağlanmazsa, hello ISO 8601 biçiminde ("o") kullanılır.|  
|adddays|Gün tooa dize zaman damgası geçirilen tamsayı sayısı ekler. Merhaba gün sayısı pozitif veya negatif olabilir. Bir biçim belirticisi sağlanmadığı sürece varsayılan olarak, hello ISO 8601 dizesinde biçimlendirin ("o"), sonucudur. Örneğin: `2015-02-23T13:27:36Z`: <p>`addseconds('2015-03-15T13:27:36Z', -20)` <p> **Numaralı parametre**: 1 <p> **Ad**: zaman damgası <p> **Açıklama**: gerekli. Başlangıç saati içeren bir dize. <p> **Numaralı parametre**: 2 <p> **Ad**: gün <p> **Açıklama**: gerekli. gün tooadd Hello sayısı. Negatif toosubtract gün olabilir. <p> **Numaralı parametre**: 3 <p> **Ad**: biçimi <p> **Açıklama**: isteğe bağlı. Ya da bir [tek bir biçim belirticisi karakter](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) veya [özel biçim deseni](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) nasıl tooformat hello bu zaman damgası değerini gösterir. Biçim sağlanmazsa, hello ISO 8601 biçiminde ("o") kullanılır.|  
|FormatDateTime|Tarih biçiminde bir dize döndürür. Bir biçim belirticisi sağlanmadığı sürece varsayılan olarak, hello ISO 8601 dizesinde biçimlendirin ("o"), sonucudur. Örneğin: `2015-02-23T13:27:36Z`: <p>`formatDateTime('2015-03-15T13:27:36Z', 'o')` <p> **Numaralı parametre**: 1 <p> **Ad**: tarih <p> **Açıklama**: gerekli. Başlangıç tarihi içeren bir dize. <p> **Numaralı parametre**: 2 <p> **Ad**: biçimi <p> **Açıklama**: isteğe bağlı. Ya da bir [tek bir biçim belirticisi karakter](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) veya [özel biçim deseni](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) nasıl tooformat hello bu zaman damgası değerini gösterir. Biçim sağlanmazsa, hello ISO 8601 biçiminde ("o") kullanılır.|  
|startOfHour|Döndürür hello geçirilen hello saat tooa dize zaman damgası başlangıcı. Örneğin `2017-03-15T13:00:00Z`:<br /><br /> `startOfHour('2017-03-15T13:27:36Z')`<br /><br /> **Numaralı parametre**: 1<br /><br /> **Ad**: zaman damgası<br /><br /> **Açıklama**: gerekli. Başlangıç saati içeren bir dize budur.<br /><br />**Numaralı parametre**: 2<br /><br /> **Ad**: biçimi<br /><br /> **Açıklama**: isteğe bağlı. Ya da bir [tek bir biçim belirticisi karakter](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) veya [özel biçim deseni](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) nasıl tooformat hello bu zaman damgası değerini gösterir. Biçim sağlanmazsa, hello ISO 8601 biçiminde ("o") kullanılır.|  
|startOfDay|Döndürür hello geçirilen hello gün tooa dize zaman damgası başlangıcı. Örneğin `2017-03-15T00:00:00Z`:<br /><br /> `startOfDay('2017-03-15T13:27:36Z')`<br /><br /> **Numaralı parametre**: 1<br /><br /> **Ad**: zaman damgası<br /><br /> **Açıklama**: gerekli. Başlangıç saati içeren bir dize budur.<br /><br />**Numaralı parametre**: 2<br /><br /> **Ad**: biçimi<br /><br /> **Açıklama**: isteğe bağlı. Ya da bir [tek bir biçim belirticisi karakter](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) veya [özel biçim deseni](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) nasıl tooformat hello bu zaman damgası değerini gösterir. Biçim sağlanmazsa, hello ISO 8601 biçiminde ("o") kullanılır.| 
|startOfMonth|Döndürür hello geçirilen hello ay tooa dize zaman damgası başlangıcı. Örneğin `2017-03-01T00:00:00Z`:<br /><br /> `startOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Numaralı parametre**: 1<br /><br /> **Ad**: zaman damgası<br /><br /> **Açıklama**: gerekli. Başlangıç saati içeren bir dize budur.<br /><br />**Numaralı parametre**: 2<br /><br /> **Ad**: biçimi<br /><br /> **Açıklama**: isteğe bağlı. Ya da bir [tek bir biçim belirticisi karakter](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) veya [özel biçim deseni](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) nasıl tooformat hello bu zaman damgası değerini gösterir. Biçim sağlanmazsa, hello ISO 8601 biçiminde ("o") kullanılır.| 
|DayOfWeek|Haftanın günü bileşenini dize zaman damgası, döndürür hello.  Pazar 0, Pazartesi 1 ve benzeri. Örneğin `3`:<br /><br /> `dayOfWeek('2017-03-15T13:27:36Z')`<br /><br /> **Numaralı parametre**: 1<br /><br /> **Ad**: zaman damgası<br /><br /> **Açıklama**: gerekli. Başlangıç saati içeren bir dize budur.| 
|DayOfMonth|Bir dize zaman damgası ay bileşenini gününü verir hello. Örneğin `15`:<br /><br /> `dayOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Numaralı parametre**: 1<br /><br /> **Ad**: zaman damgası<br /><br /> **Açıklama**: gerekli. Başlangıç saati içeren bir dize budur.| 
|DayOfYear|Bir dize zaman damgası yıl bileşenini gününü verir hello. Örneğin `74`:<br /><br /> `dayOfYear('2017-03-15T13:27:36Z')`<br /><br /> **Numaralı parametre**: 1<br /><br /> **Ad**: zaman damgası<br /><br /> **Açıklama**: gerekli. Başlangıç saati içeren bir dize budur.| 
|işaretleri|Bir dize zaman damgası özelliği döndürür hello işaretlerini. Örneğin `1489603019`:<br /><br /> `ticks('2017-03-15T18:36:59Z')`<br /><br /> **Numaralı parametre**: 1<br /><br /> **Ad**: zaman damgası<br /><br /> **Açıklama**: gerekli. Başlangıç saati içeren bir dize budur.| 
  
### <a name="workflow-functions"></a>İş akışı işlevleri  

Bu işlevler çalışma zamanında hello iş akışı kendisi hakkında bilgi almak yardımcı olur.  
  
|İşlev adı|Açıklama|  
|-------------------|-----------------|  
|listCallbackUrl|Bir dize toocall tooinvoke hello tetikleyici ya da eylem döndürür. <p> **Not**: Bu işlev yalnızca kullanılabilir bir **httpWebhook** ve **apiConnectionWebhook**, değil de bir **el ile**, **yineleme**, **http**, veya **apiConnection**. <p>Örneğin, hello `listCallbackUrl()` işlev döndürür: <p>`https://prod-01.westus.logic.azure.com:443/workflows/1235...ABCD/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=xxx...xxx` |  
|iş akışı|Bu işlev hello iş akışının kendisini hello çalışma zamanında tüm hello ayrıntıları sağlar. <p> Merhaba iş akışı nesnesindeki kullanılabilir özellikleri şunlardır: <ul><li>`name`</li><li>`type`</li><li>`id`</li><li>`location`</li><li>`run`</li></ul> <p> Merhaba hello değerini `run` aşağıdaki özelliklere sahip bir nesne özelliğidir: <ul><li>`name`</li><li>`type`</li><li>`id`</li></ul> <p>Merhaba bkz [Rest API](http://go.microsoft.com/fwlink/p/?LinkID=525617) bu özellikleri hakkında ayrıntılı bilgi için.<p> Çalıştırın, örneğin, tooget hello adını hello geçerli kullanım hello `"@workflow().run.name"` ifade. |

## <a name="next-steps"></a>Sonraki adımlar

[İş akışı eylemleri ve tetikleyicileri](logic-apps-workflow-actions-triggers.md)
