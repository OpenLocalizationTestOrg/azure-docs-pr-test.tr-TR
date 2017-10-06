---
title: "aaaCreate Resource Manager şablonu kullanarak bir Azure uygulama hizmeti ortamı"
description: "Açıklar nasıl toocreate Resource Manager şablonu kullanarak bir dış veya ILB Azure uygulama hizmeti ortamı"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu kullanarak bir ana oluşturma

## <a name="overview"></a>Genel Bakış
Azure uygulama hizmeti ortamları (ASEs), internet'ten erişilebilen bir uç nokta veya bir Azure sanal ağı (VNet) bir iç adresi noktadaki oluşturulabilir. Bir Azure tarafından bir iç yük dengeleyici (ILB) bileşeni olarak adlandırılan bir iç uç nokta oluşturulduktan sonra Bu uç sağlanır. Merhaba ana iç IP adresi üzerinde bir ILB ana adı verilir. Merhaba ana genel bir uç nokta ile bir dış ana adı verilir. 

Bir ana hello Azure portal veya bir Azure Resource Manager şablonu kullanarak oluşturulabilir. Bu makalede hello adımları ve Resource Manager şablonları ile toocreate bir dış ana ya da ILB ana ihtiyacınız sözdizimi anlatılmaktadır. toocreate bir ana hello Azure portal'ın nasıl görürüm toolearn [bir dış ana olun] [ MakeExternalASE] veya [bir ILB ana olun][MakeILBASE].

Hello Azure portalında bir ana oluşturduğunuzda, sanal ağınızı aynı saat veya önceden var olan bir VNet toodeploy içine seçin hello oluşturabilirsiniz. Bir şablondan bir ana oluşturduğunuzda ile başlamanız gerekir: 

* Resource Manager Vnet'i.
* Bu VNet içindeki bir alt ağ. Bir ana alt ağ boyutunu öneririz `/25` 128 adresleri tooaccomodate Gelecekteki büyümeyi ile. Merhaba ana oluşturulduktan sonra hello boyutunu değiştiremezsiniz.
* Sanal ağınızı Hello kaynak kimliği. Sanal ağ özellikleri altında hello Azure portal ' Bu bilgi alabilirsiniz.
* Merhaba abonelik içine toodeploy istiyor.
* toodeploy içine istediğiniz başlangıç konumu.

tooautomate ana oluşturma:

1. Merhaba ana şablon oluşturun. Bir dış ana oluşturursanız, bu adımdan sonra tamamlandı. Bir ILB ana oluşturursanız, birkaç daha fazla şey toodo vardır.

2. ILB ana oluşturulduktan sonra ILB ana etki alanı ile eşleşen bir SSL sertifikası yüklenir.

3. Merhaba karşıya yüklenen SSL sertifikası toohello ILB ana "varsayılan" SSL sertifikasını atanır.  Atanan toohello ana (örneğin, https://someapp.mycustomrootcomain.com) olan hello ortak kök etki alanı kullanırken bu sertifikayı SSL trafiği tooapps hello ILB ana üzerinde için kullanılır.


## <a name="create-hello-ase"></a>Merhaba ana oluşturma
Bir ana ve onun ilişkili parametreler dosyası oluşturur bir Resource Manager şablonu kullanılabilir [bir örnekte] [ quickstartasev2create] github'da.

Toomake bir ILB ana istiyorsanız, bu Resource Manager şablonu kullanın [örnekler][quickstartilbasecreate]. Bunlar toothat kullanım örneği karşılamak. Merhaba hello parametrelerinde çoğu *azuredeploy.parameters.json* dosyası olan ILB ASEs ve dış ASEs ortak toohello oluşturma. Merhaba aşağıdaki listede çağırır out özel not parametreleri veya bir ILB ana oluşturduğunuzda, benzersiz:

* *interalLoadBalancingMode*: Çoğu durumda, her iki HTTP/HTTPS trafiğini 80/443 numaralı bağlantı noktalarında anlamına gelir, bu too3 ayarlayın ve hello denetim/veri kanalı bağlantı noktası hello ana tooby hello FTP hizmeti kulak, ilişkili tooan ILB ayrılan sanal ağı iç adresi. Bu özellik too2 ayarlanırsa yalnızca hello FTP hizmeti ile ilgili bağlantı noktaları (Denetim ve veri kanalı) ilişkili tooan ILB adresi olur. Merhaba HTTP/HTTPS trafiğini hello ortak VIP kalır.
* *Dnssuffıx*: Bu parametre, atanan toohello ana hello varsayılan kök etki alanı tanımlar. Merhaba ortak Azure App Service içinde hello varsayılan kök etki alanı tüm web uygulamaları için çeşididir *azurewebsites.net*. Bir ILB ana iç tooa Müşteri'nin sanal ağı olduğundan, algılama toouse hello ortak hizmetin varsayılan kök etki yapmaz. Bunun yerine, bir ILB ana şirketin iç sanal ağ içinde kullanmak için anlamlı bir varsayılan kök etki alanı olmalıdır. Örneğin, Contoso Corporation bir varsayılan kök etki alanı kullanabilirsiniz *contoso.com iç* hedeflenen toobe çözümlenebilir ve yalnızca Contoso sanal ağ içinde erişilebilir olan uygulamalar. 
* *ipSslAddressCount*: Bu parametre 0'hello tooa değeri otomatik olarak varsayılan olarak *azuredeploy.json* ILB ASEs yalnızca tek bir ILB adresine sahip olmadığından dosya. Hiçbir açık bir ILB ana IP SSL adresleri vardır. Bu nedenle, hello IP SSL adres havuzu için bir ILB ana toozero ayarlamanız gerekir. Aksi halde, bir sağlama hatası oluşur. 

Merhaba sonra *azuredeploy.parameters.json* dosya doldurulur, hello ana hello PowerShell kod parçacığını kullanarak oluşturun. Merhaba dosya yolları toomatch hello Resource Manager şablonu dosya konumlarını makinenizde değiştirin. Toosupply hello Resource Manager dağıtım adını ve hello kaynak grubu adı için kendi değerlerinizi unutmayın:

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Yaklaşık hello ana toobe oluşturulan bir saat sürer. Ardından hello ana listesinde hello ASEs hello dağıtım tetiklenen hello abonelik için hello portalında görünür.

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>Karşıya yükleme ve hello "varsayılan" SSL sertifikası yapılandırma
Bir SSL sertifikası kullanılan tooestablish SSL bağlantılarını tooapps hello "varsayılan" SSL sertifikası hello ana ile ilişkilendirilmiş olması gerekir. Merhaba ana'nın varsayılan DNS son eki ise *contoso.com iç*, bağlantı toohttps://some-random-app.internal-contoso.com için geçerli bir SSL sertifikası gerektirir **.internal contoso.com* . 

İç sertifika yetkilileri kullanarak, bir dış veren bir sertifika satın veya otomatik olarak imzalanan bir sertifika kullanarak geçerli bir SSL sertifikası alın. Bağımsız olarak Hello kaynak hello SSL sertifikasının sertifika öznitelikleri aşağıdaki hello düzgün şekilde yapılandırılmalıdır:

* **Konu**: Bu özniteliği çok ayarlanmalıdır **kök etki alanı here.com .your*.
* **Konu alternatif adı**: Bu öznitelik her ikisini de içermelidir **kök etki alanı here.com .your* ve **.scm.your-kök-etki-here.com*. SSL bağlantıları toohello SCM/Kudu site her uygulamayla ilişkili hello formunun bir adres kullanın *your-app-name.scm.your-root-domain-here.com*.

Elle içinde geçerli bir SSL sertifikası ile iki ek hazırlık adımları gereklidir. Convert/hello SSL sertifikası bir .pfx dosyası olarak Kaydet. Bu hello .pfx dosyasını tüm ara içerir ve sertifikaları kök unutmayın. Bir parola ile güvenli hale getirin.

Merhaba .pfx dosyasını hello SSL sertifikası bir Resource Manager şablonu kullanarak yüklendiği bir base64 dizeye dönüştürülen toobe gerekir. Resource Manager şablonları metin dosyaları olduğundan hello .pfx dosyasını bir base64 dizeye dönüştürülmesi gerekir. Bu şekilde hello şablon parametresi olarak dahil edilebilir.

PowerShell kod parçacığını aşağıdaki hello kullan:

* Otomatik olarak imzalanan bir sertifika oluşturun.
* Merhaba sertifika .pfx dosyası olarak dışarı aktarın.
* Merhaba .pfx dosyası base64 ile kodlanmış bir dizeye dönüştürün.
* Merhaba base64 ile kodlanmış dize tooa ayrı bir dosyaya kaydedin. 

Base64 kodlaması için bu PowerShell kodu hello uyarlanmıştır [PowerShell komut dosyası blog][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Merhaba SSL sertifikası başarıyla oluşturuldu ve dönüştürülen tooa base64 ile kodlanmış dize sonra hello örnek Resource Manager şablonu kullanmak [yapılandırma hello varsayılan SSL sertifikasını] [ quickstartconfiguressl] github'da. 

Merhaba hello parametrelerinde *azuredeploy.parameters.json* dosya burada listelenir:

* *appServiceEnvironmentName*: Merhaba ILB yapılandırılan ana hello adı.
* *existingAseLocation*: metin dizesini içeren hello burada hello ILB ana dağıtılan Azure bölgesi.  Örneğin: "Orta Güney ABD".
* *pfxBlobString*: Merhaba hello .pfx dosyasını based64 kodlanmış bir dize gösterimi. Daha önce gösterilen hello kod parçacığını kullanın ve "exportedcert.pfx.b64" içinde yer alan hello dizesini kopyalayın. Merhaba hello değeri olarak yapıştırmak *pfxBlobString* özniteliği.
* *Parola*: hello kullanılan parola toosecure hello .pfx dosyası.
* *certificateThumbprint*: sertifikanın parmak izi hello. Bu değer Powershell'den alırsanız (örneğin, *$certificate. Parmak izi* hello'den önceki kod parçacığını), olduğu gibi hello değer kullanabilirsiniz. Merhaba Windows sertifika iletişim kutusundan hello değeri kopyalarsanız, hello gereksiz boşluklar çıkışı toostrip unutmayın. Merhaba *certificateThumbprint* AF3143EB61D43F6727842115BB7F17BBCECAECAE gibi görünmelidir.
* *certificateName*: kendi seçme kolay dize tanımlayıcı tooidentity hello sertifika kullanılır. Merhaba adı Merhaba hello benzersiz Resource Manager tanımlayıcı bir parçası olarak kullanılan *Microsoft.Web/certificates* hello SSL sertifikası temsil eden varlık. Merhaba adı *gerekir* soneki aşağıdaki hello ile bitmelidir: \_yourASENameHere_InternalLoadBalancingASE. kullanılan toosecure bir ILB özellikli ana sertifika hello bir göstergesi olduğu gibi hello Azure portal bu soneki kullanır.

Kısaltılmış örneği *azuredeploy.parameters.json* burada gösterilir:

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

Merhaba sonra *azuredeploy.parameters.json* dosya doldurulur, hello varsayılan SSL sertifikasını hello PowerShell kod parçacığını kullanarak yapılandırın. Merhaba Resource Manager şablonu dosyalarını makinenizde bulunduğu hello dosya yolları toomatch değiştirin. Toosupply hello Resource Manager dağıtım adını ve hello kaynak grubu adı için kendi değerlerinizi unutmayın:

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Ana ön uç tooapply hello değişiklik başına kabaca 40 dakika sürer. Örneğin, iki ön uçlar kullanan bir varsayılan boyutlu ana için bir saat ve 20 dakika toocomplete hello şablonunu alır. Merhaba şablon çalışırken hello ana ölçeklendirme olamaz.  

Merhaba şablon bittikten sonra hello ILB ana uygulamaları HTTPS üzerinden erişilebilir. Merhaba bağlantıları hello varsayılan SSL sertifikası kullanılarak güvenli hale getirilir. Merhaba ILB ana uygulamaları hello uygulama adına ve hello varsayılan ana bilgisayar adı bir bileşimini kullanarak ele alınan hello varsayılan SSL sertifikası kullanılır. Örneğin, https://mycustomapp.internal-contoso.com hello varsayılan SSL sertifikası için kullanması **.internal contoso.com*.

Ancak, hello ortak çok müşterili hizmeti Çalıştır yalnızca gibi uygulamalar, geliştiriciler özel ana bilgisayar adları tek tek uygulamalar için yapılandırabilirsiniz. Bunlar benzersiz SNI SSL sertifikası bağlamaları tek tek uygulamalar için de yapılandırabilirsiniz.

## <a name="app-service-environment-v1"></a>App Service Ortamı v1 ##
Uygulama hizmeti ortamı iki sürümü vardır: ASEv1 ve ASEv2. Önceki bilgilere hello üzerinde ASEv2 dayanır. Bu bölümde ASEv1 ve ASEv2 arasındaki farklar hello gösterir.

ASEv1 içinde tüm hello kaynakları el ile yönetin. Merhaba ön uçları, çalışanlar ve IP tabanlı SSL için kullanılan IP adresleri dahildir. Uygulama hizmeti planınızı ölçeklendirebilirsiniz önce onu toohost istediğiniz hello çalışan havuzunda Ölçeklendirmesi gerekir.

ASEv1 ASEv2 öğesinden farklı bir fiyatlandırma modelini kullanır. ASEv1 içinde ayrılmış her çekirdek için ücret ödersiniz. Ön Uçları veya tüm iş yükleri barındıran olmayan çalışanlar için kullanılan çekirdek dahildir. ASEv1 içinde hello varsayılan en büyük ölçekli bir ana boyutunu 55 toplam konakları ' dir. Bu, çalışanlar ve ön uçlar içerir. Bu bir Klasik sanal ağı ve Resource Manager sanal ağ içinde dağıtılabilir bir avantajı tooASEv1 olur. toolearn ASEv1, hakkında daha fazla bilgi görmek [uygulama hizmeti ortamı v1 giriş][ASEv1Intro].

Resource Manager şablonu kullanarak bir ASEv1 toocreate bkz [Resource Manager şablonu ile bir ILB ana v1 oluşturma][ILBASEv1Template].


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
