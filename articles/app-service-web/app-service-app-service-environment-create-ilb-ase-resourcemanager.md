---
title: "aaaHow tooCreate bir ILB ana kullanarak Azure Resource Manager şablonları | Microsoft Docs"
description: "Nasıl toocreate bir iç yük dengeleyici ana Azure Resource Manager şablonları kullanarak öğrenin."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>Nasıl tooCreate bir ILB ana kullanarak Azure Resource Manager şablonları

> [!NOTE] 
> Uygulama hizmeti ortamı v1 hello hakkında makaledir. Merhaba, daha kolay toouse ve daha güçlü altyapısı üzerinde çalışan uygulama hizmeti ortamı'nın daha yeni bir sürümü var. Merhaba yeni sürümü hakkında daha fazla ile Merhaba Başlat toolearn [giriş toohello uygulama hizmeti ortamı](../app-service/app-service-environment/intro.md).
>

## <a name="overview"></a>Genel Bakış
Uygulama hizmeti ortamları, genel VIP yerine bir sanal ağ iç adresiyle oluşturulabilir.  Bu iç adresi hello iç yük dengeleyiciye (ILB) adlı bir Azure bir bileşen tarafından sağlanır.  Bir ILB ana hello Azure portal kullanarak oluşturulabilir.  Bu, Azure Resource Manager şablonları yapmamanız otomasyonu kullanarak da oluşturulabilir.  Bu makalede hello adımlarda size yol gösterir ve sözdizimi toocreate ILB ana Azure Resource Manager şablonları ile gerekli.

Bir ILB ana oluşturulmasını otomatik hale getirmede ilgili üç adım vardır:

1. İlk hello temel ana ortak bir VIP yerine bir iç yük dengeleyici adresi kullanarak bir sanal ağ içinde oluşturulur.  Bu adım bir parçası olarak, bir kök etki alanı adı toohello ILB ana atanır.
2. ILB ana oluşturulan hello bir SSL sertifikası yüklendikten sonra.  
3. Merhaba karşıya yüklenen SSL sertifikası açıkça toohello ILB ana "varsayılan" SSL sertifikasını atanır.  Merhaba ortak kök etki alanına atanan toohello ana (örneğin https://someapp.mycustomrootcomain.com) kullanarak Hello uygulamaları ele olduğunda bu SSL sertifikasını SSL trafiği tooapps hello ILB ana üzerinde kullanılır

## <a name="creating-hello-base-ilb-ase"></a>Merhaba temel ILB ana oluşturma
Bir örnek Azure Resource Manager şablonunu ve ilişkili parametreler dosyası, Github'da bulunan [burada][quickstartilbasecreate].

Merhaba hello parametrelerinde çoğu *azuredeploy.parameters.json* dosya ortak toocreating hem ILB ASEs yanı sıra tooa genel VIP ASEs bağlı olan.  out Parametreleri özel notunun çağrıları aşağıdaki Hello liste veya bir ILB ana oluştururken benzersiz şunlardır:

* *interalLoadBalancingMode*: 80/443 numaralı bağlantı noktalarında her iki HTTP/HTTPS trafiğini anlamına gelir, bu too3 çoğu durumda ayarlamak ve hello denetim/veri kanalı bağlantı noktası kulak hello ana tooby hello FTP hizmeti, ilişkili tooan ILB sanal ağ ayrılır iç adresi.  Bağlantı noktaları (Denetim ve veri kanalı) bağlı yalnızca hello FTP hizmeti ile ilgili daha sonra bu özellik too2, bunun yerine ayarlanırsa tooan ILB adres, hello HTTP/HTTPS trafiğini hello ortak VIP kalırken.
* *Dnssuffıx*: Bu parametre toohello ana atanacak hello varsayılan kök etki alanını tanımlar.  Merhaba ortak Azure App Service içinde hello varsayılan kök etki alanı tüm web uygulamaları için çeşididir *azurewebsites.net*.  Ancak bir ILB ana iç tooa Müşteri'nin sanal ağ olduğundan, algılama toouse hello ortak hizmetin varsayılan kök etki yapmaz.  Bunun yerine, bir ILB ana şirketin iç sanal ağ içinde kullanmak için anlamlı bir varsayılan kök etki alanı olmalıdır.  Örneğin, bir varsayılan kök etki alanı kuramsal Contoso Corporation kullanabilirsiniz *contoso.com iç* çözümlenebilir ve Contoso sanal ağ içinde erişilebilir hedeflenen tooonly uygulamalar için. 
* *ipSslAddressCount*: Bu parametre otomatik olarak 0'hello tooa değerini varsayılan *azuredeploy.json* ILB ASEs yalnızca tek bir ILB adresine sahip olmadığından dosya.  Hiçbir açık bir ILB ana IP SSL adresleri vardır ve bu nedenle hello IP SSL adres havuzu için bir ILB ana toozero, aksi takdirde bir sağlama hatası ortaya çıkar ayarlanması gerekir. 

Bir kez hello *azuredeploy.parameters.json* dosya doldurulmuş bir ILB ana için hello ILB ana sonra Powershell kod parçacığını aşağıdaki hello kullanılarak oluşturulabilir.  Hello Azure Resource Manager şablonu dosyalarını makinenizde bulunduğu hello dosya yolları toomatch değiştirin.  Ayrıca toosupply hello Azure Resource Manager dağıtım adını ve kaynak grubu adı için kendi değerlerinizi unutmayın.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Merhaba sonra Azure Resource Manager Şablonu oluşturulan hello ILB ana toobe için birkaç saat sürecek gönderilir.  Hello oluşturma tamamlandıktan sonra uygulama hizmeti ortamları hello listesinde hello dağıtım tetiklenen hello abonelik için UX hello portalında hello ILB ana görünecektir.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>Karşıya yükleme ve hello "Varsayılan" SSL sertifikası yapılandırma
Bir kez hello, ILB ana oluşturulmuş bir SSL sertifikası SSL bağlantılarını tooapps kurmak için SSL sertifika kullanımı hello "varsayılan" olarak hello ana ile ilişkili olmalıdır.  DNS Hello ana'nın varsayılan hello kuramsal Contoso Corporation örnekle devam edersek sonekidir *contoso.com iç*, ardından bağlantı çok*https://some-random-app.internal-contoso.com*için geçerli bir SSL sertifikası gerektirir **.internal contoso.com*. 

İç CA'lar da dahil olmak üzere, bir dış veren bir sertifika satın alma ve kendinden imzalı bir sertifika kullanarak geçerli bir SSL sertifikası yolları tooobtain çeşitli vardır.  Bağımsız olarak Hello kaynak hello SSL sertifikasının hello aşağıdaki sertifika öznitelikleri düzgün yapılandırılmış toobe gerekir:

* *Konu*: Bu özniteliği çok ayarlanmalıdır **kök etki alanı here.com .your*
* *Konu alternatif adı*: Bu öznitelik her ikisini de içermelidir **kök etki alanı here.com .your*, ve **.scm.your-kök-etki-here.com*.  Merhaba hello ikinci giriş hello formunun bir adresi kullanarak her uygulamayla ilişkili SCM/Kudu site oluşturulacak bu SSL bağlantılarını toohello nedeni *your-app-name.scm.your-root-domain-here.com*.

Elle içinde geçerli bir SSL sertifikası ile iki ek hazırlık adımları gereklidir.  bir .pfx dosyası olarak dönüştürülen/kaydedilen toobe Hello SSL sertifikası gerekir.  Bu hello .pfx dosyasını tooinclude tüm ara ve kök sertifikaları gerekir ve ayrıca bir parolayla korunan toobe gerekir unutmayın.

Ardından hello sonuç .pfx dosyasını hello SSL sertifikası bir Azure Resource Manager şablonu kullanarak karşıya yüklenecek çünkü bir base64 dizeye dönüştürülen toobe gerekir.  Azure Resource Manager şablonları metin dosyaları olduğundan, hello .pfx dosyasını hello şablon parametresi olarak dahil edilebilir şekilde bir base64 dizeye dönüştürülen toobe gerekir.

otomatik olarak imzalanan sertifika oluşturma örneği Hello Powershell kod parçacığı aşağıda gösterilmiştir, hello sertifika verme bir .pfx dosyası olarak dize kodlanmış bir base64 hello .pfx dosyasını dönüştürme ve kodlanmış dize tooa ayrı bir dosya hello base64 kaydetme.  Base64 kodlaması hello uyarlanmıştır için Powershell kodu hello [Powershell komut dosyaları Blog][examplebase64encoding].

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

Merhaba SSL sertifikası başarıyla oluşturuldu ve dönüştürülen tooa Base64 ile kodlanmış dize sonra örnek Azure Resource Manager şablonu için github'da hello [hello varsayılan SSL sertifikası yapılandırma] [ configuringDefaultSSLCertificate] kullanılabilir.

Merhaba hello parametrelerinde *azuredeploy.parameters.json* dosya aşağıda listelenmiştir:

* *appServiceEnvironmentName*: Merhaba ILB yapılandırılan ana hello adı.
* *existingAseLocation*: metin dizesini içeren hello burada hello ILB ana dağıtılan Azure bölgesi.  Örneğin: "Orta Güney ABD".
* *pfxBlobString*: Merhaba based64 kodlanmış hello .pfx dosyasını dize gösterimi.  Daha önce gösterilen hello kod parçacığını kullanarak kopyalayın hello dizesi "exportedcert.pfx.b64" içinde yer alan ve hello hello değeri olarak yapıştırmak *pfxBlobString* özniteliği.
* *Parola*: hello kullanılan parola toosecure hello .pfx dosyası.
* *certificateThumbprint*: sertifikanın parmak izi hello.  Bu değer Powershell'den alırsanız (örneğin *$certificate. Parmak izi* hello öğesinden önceki kod parçacığını), başlangıç değeri olarak kullanabilirsiniz-olduğu.  Merhaba Windows sertifika iletişim kutusundan hello değeri kopyalarsanız, ancak hello gereksiz boşluklar çıkışı toostrip unutmayın.  Merhaba *certificateThumbprint* gibi görünmelidir: AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *certificateName*: kendi seçme kolay dize tanımlayıcı tooidentity hello sertifika kullanılır.  Merhaba adı Merhaba hello benzersiz Azure Resource Manager tanımlayıcı bir parçası olarak kullanılan *Microsoft.Web/certificates* hello SSL sertifikası temsil eden varlık.  Merhaba adı **gerekir** soneki aşağıdaki hello ile bitmelidir: \_yourASENameHere_InternalLoadBalancingASE.  Sertifika hello bir gösterge bir ILB özellikli ana güvenliğini sağlamak için kullanılan bu sonek hello portal tarafından kullanılır.

Kısaltılmış örneği *azuredeploy.parameters.json* aşağıda gösterilmiştir:

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Bir kez hello *azuredeploy.parameters.json* dosya doldurulmuş, hello varsayılan SSL sertifikasını Powershell kod parçacığını aşağıdaki hello kullanılarak yapılandırılabilir.  Hello Azure Resource Manager şablonu dosyalarını makinenizde bulunduğu hello dosya yolları toomatch değiştirin.  Ayrıca toosupply hello Azure Resource Manager dağıtım adını ve kaynak grubu adı için kendi değerlerinizi unutmayın.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Merhaba sonra Azure Resource Manager şablonu kabaca ana ön uç tooapply hello değişiklik başına kırk dakika dakika sürer gönderilir.  Örneğin, varsayılan olarak iki ön uç kullanarak boyutlu ana hello şablonu bir saat ve dakika toocomplete yirmi etrafında olur.  Merhaba şablon çalışırken hello ana mümkün tooscaled olmaz.  

Merhaba şablon işlemi tamamlandıktan sonra hello ILB ana uygulamaları HTTPS üzerinden erişilebilir ve hello bağlantıları güvenli hello varsayılan SSL sertifikası.  Merhaba uygulama adına ve hello varsayılan konak adını kullanan uygulamaların hello ILB ana ele zaman hello varsayılan SSL sertifikası kullanılır.  Örneğin *https://mycustomapp.internal-contoso.com* hello varsayılan SSL sertifikası için kullanacağınız **.internal contoso.com*.

Ancak, hello ortak çok kiracılı hizmetinde çalışan yalnızca gibi uygulamalar, geliştiriciler özel ana bilgisayar adları tek tek uygulamalar için de yapılandırmanız ve benzersiz SNI SSL sertifikası bağlamaları tek tek uygulamalar için yapılandırın.  

## <a name="getting-started"></a>Başlarken
Uygulama hizmeti ortamları ile çalışmaya tooget bakın [giriş tooApp hizmeti ortamı](app-service-app-service-environment-intro.md)

Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

