---
title: "DevTest Labs VM için özel yapılar aaaCreate | Microsoft Docs"
description: "Tooauthor kendi yapıtlar için DevTest Labs ile kullanma hakkında bilgi edinin"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>DevTest Labs VM için özel yapılar oluşturma
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Genel Bakış
**Yapıları** kullanılan toodeploy olan ve bir VM sağlandıktan sonra uygulamanızı yapılandırın. Yapı tanımı dosyası ve bir git deposu klasöründe depolanan diğer komut dosyalarını bir yapı oluşur. Yapı tanımı dosyaları oluşur JSON ve istediğiniz toospecify kullanabileceğiniz ifadeler bir VM'de tooinstall. Örneğin, bir yapı, komut toorun ve hello komutu çalıştırdığınızda, kullanılabilir hale getirilir parametreleri hello adını tanımlayabilirsiniz. Ada göre tooother komut dosyaları hello yapı tanımı dosyasındaki başvurabilir.

## <a name="artifact-definition-file-format"></a>Yapı tanımı dosyası biçimi
Merhaba aşağıdaki örnek hello temel bir tanım dosyası yapınızı olun hello bölümleri gösterir:

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| Öğe adı | Gerekli mi? | Açıklama |
| --- | --- | --- |
| $schema |Hayır |Merhaba tanım dosyası hello geçerliliğini sınamada yardımcı hello JSON Şeması dosyasının konumu. |
| Başlık |Evet |Merhaba laboratuvarda görüntülenen hello yapı adı. |
| açıklama |Evet |Merhaba laboratuvarda görüntülenen hello yapı açıklaması. |
| iconUri |Hayır |Merhaba simgesi hello laboratuvarda görüntülenir URI'si. |
| targetOsType |Evet |Merhaba VM yapıt yüklendiği işletim sistemi. Desteklenen Seçenekler şunlardır: Windows ve Linux. |
| parametreler |Hayır |Bir makinede yapı yükleme komutunu çalıştırdığınızda, sağlanan değerler. Bu, yapı özelleştirme yardımcı olur. |
| KomutÇalıştır |Evet |Yapı bir VM üzerinde yürütülen komutu yükleyin. |

### <a name="artifact-parameters"></a>Yapı parametreleri
Merhaba Parametreler bölümünde hello tanım dosyası, bir kullanıcı bir yapı yüklerken giriş hangi değerlerini belirtin. Merhaba yapı yükleme komut toothese değerleri başvurabilir.

Yapı izlenerek hello ile parametrelerini tanımlayın:

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Öğe adı | Gerekli mi? | Açıklama |
| --- | --- | --- |
| type |Evet |Parametre değeri türü. Liste türleri izin hello için aşağıdaki hello bakın: |
| Görünen adı |Evet |Görüntülenen tooa kullanıcı hello laboratuarda hello parametresinin adı. | |
| açıklama |Evet |Merhaba laboratuvarda görüntülenen hello parametre açıklaması. |

Merhaba izin verilen türleri şunlardır:

* dize – geçerli bir JSON dize
* int – geçerli bir JSON tamsayı
* bool – geçerli bir JSON Boole
* dizi – geçerli bir JSON dizisi

## <a name="artifact-expressions-and-functions"></a>Yapı ifadeleri ve İşlevler
İşlevler tooconstruct hello yapı yükleme komutunu ve ifade kullanabilirsiniz.
İfadeler ile parantez içine ([ve]) ve hello yapı yüklendiğinde değerlendirilir. İfadeler bir JSON dizesi değerindeki herhangi bir yerde görünür ve her zaman başka bir JSON değeri döndürür. Toouse köşeli ayraç ile başlayan bir sabit dize gerekip gerekmediğini [, iki ayraç kullanmalısınız [[.
Genellikle, ifadeler işlevleri tooconstruct bir değer kullanın. JavaScript'te, gibi işlev çağrılarını functionName(arg1,arg2,arg3) biçimlendirilir.

Merhaba aşağıdaki listede ortak işlevleri gösterilmektedir:

* parameters(parameterName) - hello yapı komutu çalıştırdığınızda, sağlanan bir parametre değeri döndürür.
* concat (arg1, arg2, arg3,...) - birden çok dize değerlerini birleştirir. Bu işlev bağımsız değişkenleri herhangi bir sayıda alabilir.

örnekte gösterildiği nasıl aşağıdaki hello toouse ifadesi ve işlevleri tooconstruct bir değer:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Özel yapı oluşturma
Özel yapı, aşağıdaki adımları izleyerek oluşturun:

1. Bir JSON Düzenleyicisi yükleme - yapı tanım dosyalarını bir JSON Düzenleyicisi toowork gerekir. Kullanmanızı öneririz [Visual Studio Code](https://code.visualstudio.com/), Windows, Linux ve OS X için kullanılabilir olduğu.
2. Azure DevTest Labs ekibi tarafından oluşturulan bir örnek artifactfile.json - hello yapıları kullanıma alma bizim [GitHub deposunu](https://github.com/Azure/azure-devtestlab), zengin denetim kitaplığı oluşturduk burada yardımcı yapıları kendi yapıları oluşturun. Yapı tanımı dosyasını indirin ve kendi yapıları değişiklikleri tooit toocreate olun.
3. IntelliSense - kullanılan tooconstruct olabilir Dengeleme IntelliSense toosee geçerli öğeleri bir yapı tanımı dosyası yararlanır. Merhaba, bir öğenin değerleri için farklı seçenekler de görebilirsiniz. Örneğin, size hello iki seçenek Windows veya Linux hello düzenlerken IntelliSense'i Göster **targetOsType** öğesi.
4. Mağaza hello yapı içinde bir [git deposu](devtest-lab-add-artifact-repo.md).
   
   1. Burada hello dizin adı olduğu hello aynı hello yapı adı olarak her bir yapı için ayrı bir dizin oluşturun.
   2. Merhaba yapı tanım dosyası (artifactfile.json), oluşturduğunuz hello dizinde depolayın.
   3. Hello yapıdan başvurulan deposu hello komut dosyaları yükleme komutu.
      
      Yapı klasörü nasıl görünebileceği örnek aşağıda verilmiştir:
      
      ![Yapı git deposuna örnek](./media/devtest-lab-artifact-author/git-repo.png)
5. Merhaba yapıları depo toohello Laboratuvar add - toohello makalesine başvurun [yapıları ve şablonlar için Git deposu ekleme](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>İlgili makaleler
* [Nasıl DevTest Labs de toodiagnose yapı hataları](devtest-lab-troubleshoot-artifact-failure.md)
* [VM tooexisting AD Azure DevTest Labs'de resource manager şablonu kullanarak etki alanına katılma](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[Git yapıt deposu tooa Laboratuvar ekleme](devtest-lab-add-artifact-repo.md).

