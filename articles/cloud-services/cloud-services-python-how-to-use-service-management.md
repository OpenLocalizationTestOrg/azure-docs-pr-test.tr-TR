---
title: "aaaHow toouse hello Hizmet Yönetimi API'si (Python) - özellik Kılavuzu"
description: "Nasıl tooprogrammatically ortak hizmet yönetim görevleri gerçekleştirebilir Python öğrenin."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a>Nasıl toouse python'dan Hizmet Yönetimi
Bu kılavuz size nasıl tooprogrammatically ortak hizmet yönetim görevleri gerçekleştirebilir Python gösterir. Merhaba **ServiceManagementService** hello sınıfında [Python için Azure SDK](https://github.com/Azure/azure-sdk-for-python) programlı erişim toomuch hello kullanılabilirhelloservisyönetimiyleilgiliişlevselliğidestekler[Klasik azure portalı] [ management-portal] (gibi **oluşturma, güncelleştirme ve bulut Hizmetleri, dağıtımları, Veri Yönetimi Hizmetleri ve sanal makineleri silme**). Bu işlev programlı erişim tooservice yönetim ihtiyaç duyan uygulamalar oluşturmada faydalı olabilir.

## <a name="WhatIs"></a>Hizmet yönetimi nedir
Merhaba Hizmet Yönetimi API'si sağlar hello hello kullanılabilen hizmet yönetim işlevlerinin programlı erişim toomuch [Klasik Azure portalı][management-portal]. Merhaba Python için Azure SDK toomanage sağlayan bulut Hizmetleri ve depolama hesapları.

toouse hello Hizmet Yönetimi API'si, gereksinim duyduğunuz çok[bir Azure hesabı oluşturma](https://azure.microsoft.com/pricing/free-trial/).

## <a name="Concepts"></a>Kavramları
Merhaba Python için Azure SDK sarmalar hello [Azure Hizmet Yönetimi API'si][svc-mgmt-rest-api], REST API olduğu. Tüm API işlemleri SSL üzerinden gerçekleştirilir ve X.509 v3 sertifikaları kullanılarak karşılıklı kimlik doğrulaması yapılır. Merhaba Yönetim Hizmeti gelen içinde Azure veya hello Internet üzerinden doğrudan bir HTTPS isteği göndermek ve bir HTTPS yanıt herhangi bir uygulamadan çalışan bir hizmete erişebilir.

## <a name="Installation"></a>Yükleme
Bu makalede açıklanan tüm hello özellikleri hello kullanılabilir `azure-servicemanagement-legacy` paketi olarak PIP kullanarak yükleyebilirsiniz. Bu makalede (örneğin, yeni tooPython varsa) yükleme hakkında daha fazla bilgi için bkz: [yükleme Python ve hello Azure SDK'sı](../python-how-to-install.md)

## <a name="Connect"></a>Nasıl yapılır: tooservice Yönetimi bağlama
tooconnect toohello Hizmet Yönetimi uç nokta, Azure abonelik Kimliğinizi ve geçerli bir yönetim sertifikası gerekir. Abonelik Kimliğinizi hello aracılığıyla elde edebilirsiniz [Klasik Azure portalı][management-portal].

> [!NOTE]
> Bu olası toouse sertifikaları Windows üzerinde çalışan OpenSSL ile oluşturulan sunulmuştur.  Python 2.7.4 gerektirir veya sonraki bir sürümü. .Pfx sertifikaları büyük ihtimalle hello gelecekte kaldırılacaktır desteği itibaren .pfx, yerine kullanıcıların toouse OpenSSL öneririz.
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Yönetim sertifikaları Windows/Mac/Linux (OpenSSL)
Kullanabileceğiniz [OpenSSL](http://www.openssl.org/) toocreate yönetim sertifikası.  Gerçekte toocreate iki sertifika, hello sunucu için bir tane gerekir (bir `.cer` dosyası) hello istemci için bir tane (bir `.pem` dosyası). toocreate hello `.pem` dosya, yürütün:

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

toocreate hello `.cer` sertifika, yürütün:

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

Azure sertifikaları hakkında daha fazla bilgi için bkz: [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md). OpenSSL parametreler tam bir açıklaması için hello belgelerine bakın [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).

Bu dosyalar oluşturduktan sonra tooupload hello gereksinim `.cer` tooAzure hello "Karşıya Yükle" eylemin hello hello "Ayarlar" sekmesini aracılığıyla dosya [Klasik Azure portalı][management-portal], ve toomake Not gerekiyor Merhaba kaydettiğiniz `.pem` dosya.

Abonelik Kimliğinizi aldıktan sonra bir sertifika oluşturulur ve hello karşıya `.cer` dosya tooAzure hello abonelik kimliği ve hello yolu toohello geçirerek toohello Azure yönetim uç noktasına bağlanabilir `.pem` çok dosya**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

Örneğin, önceki hello içinde `sms` olan bir **ServiceManagementService** nesnesi. Merhaba **ServiceManagementService** sınıfı hello kullanılan birincil sınıf toomanage Azure hizmetleridir.

### <a name="management-certificates-on-windows-makecert"></a>Yönetim sertifikaları Windows (MakeCert)
Otomatik imzalı yönetim sertifikası, makine kullanarak oluşturabileceğiniz `makecert.exe`.  Açık bir **Visual Studio komut istemi** olarak bir **yönetici** ve aşağıdaki komut, değiştirme hello *AzureCertificate* gibi hello sertifika adına sahip toouse.

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

Merhaba komut oluşturur hello `.cer` dosya ve hello yükler **kişisel** sertifika deposu. Daha fazla bilgi için bkz: [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md).

Merhaba sertifika oluşturduktan sonra tooupload hello gereksinim `.cer` tooAzure hello "Karşıya Yükle" eylemin hello hello "Ayarlar" sekmesini aracılığıyla dosya [Klasik Azure portalı][management-portal].

Abonelik Kimliğinizi aldıktan sonra bir sertifika oluşturulur ve hello karşıya `.cer` dosya tooAzure hello abonelik kimliği ve hello sertifika hello konumunu, geçirerektoohelloAzureyönetimuçnoktasınabağlanabilir**Kişisel** çok sertifika deposunu**ServiceManagementService** (yeniden Değiştir *AzureCertificate* sertifikanızın hello adıyla):

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

Örneğin, önceki hello içinde `sms` olan bir **ServiceManagementService** nesnesi. Merhaba **ServiceManagementService** sınıfı hello kullanılan birincil sınıf toomanage Azure hizmetleridir.

## <a name="ListAvailableLocations"></a>Nasıl yapılır: kullanılabilir konumlarını listeleyin
hizmetlerini barındırmak için kullanılabilir toolist hello konumlarını kullanın hello **listesi\_konumları** yöntemi:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

Bir bulut hizmeti veya depolama hizmeti oluşturduğunuzda tooprovide geçerli bir konum gerekir. Merhaba **listesi\_konumları** yöntem her zaman güncel bir hello şu anda kullanılabilir konumların listesini döndürür. Bu makalenin yazıldığı sırada hello kullanılabilir konumlarını şunlardır:

* Batı Avrupa
* Kuzey Avrupa
* Güneydoğu Asya
* Doğu Asya
* Orta ABD
* Orta Kuzey ABD
* Orta Güney ABD
* Batı ABD
* Doğu ABD
* Japonya Doğu
* Japonya Batı
* Güney Brezilya
* Avustralya Doğu
* Avustralya Güneydoğu

## <a name="CreateCloudService"></a>Nasıl yapılır: bir bulut hizmeti oluştur
Bir uygulama oluşturduğunuzda ve Azure'da çalıştırmak, hello kod ve yapılandırma birlikte Azure adlandırılır [bulut hizmeti] [ cloud service] (olarak bilinen bir *barındırılan hizmetin* içinde daha önce Azure serbest bırakır). Merhaba **oluşturma\_barındırılan\_hizmet** yöntemi verir toocreate yeni bir barındırılan hizmet (hangi Azure içinde benzersiz olması gerekir) barındırılan hizmet adını sağlayarak bir etiket (otomatik olarak kodlanmış toobase64), bir Açıklama ve bir konum.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

Tüm hello barındırılan hizmetler hello aboneliğinizle için listeleyebilirsiniz **listesi\_barındırılan\_Hizmetleri** yöntemi:

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

Belirli bir barındırılan hizmet tooget öğrenmek istiyorsanız, bunu hello barındırılan hizmet adı toohello geçirerek yapabilirsiniz **almak\_barındırılan\_hizmet\_özellikleri** yöntemi:

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

Bir bulut hizmeti oluşturduktan sonra kodu toohello hizmetiniz hello ile dağıtabilirsiniz **oluşturma\_dağıtım** yöntemi.

## <a name="DeleteCloudService"></a>Nasıl yapılır: bir bulut hizmetini silin
Merhaba hizmet adı toohello geçirerek bir bulut hizmeti silebilirsiniz **silmek\_barındırılan\_hizmet** yöntemi:

    sms.delete_hosted_service('myhostedservice')

Bir hizmet silmeden önce hello hizmeti için tüm dağıtımlar silinmesi gerekir. (Bkz [nasıl yapılır: bir dağıtımı silin](#DeleteDeployment) Ayrıntılar için.)

## <a name="DeleteDeployment"></a>Nasıl yapılır: bir dağıtımı silin
toodelete bir dağıtımı kullanmak hello **silmek\_dağıtım** yöntemi. Merhaba aşağıdaki örnek bir dağıtım toodelete nasıl adlı gösterir `v1`.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"></a>Nasıl yapılır: bir depolama birimi hizmeti oluşturma
A [depolama birimi hizmeti](../storage/common/storage-create-storage-account.md) , tooAzure erişmenizi [BLOB'lar](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabloları](../cosmos-db/table-storage-how-to-use-python.md), ve [sıraları](../storage/queues/storage-python-how-to-use-queue-storage.md). bir depolama birimi hizmeti toocreate hello hizmeti (3 ila 24 küçük harf karakter ve Azure içinde benzersiz) için bir ad, açıklama, bir etiket (yukarı too100 karakter, otomatik olarak kodlanmış toobase64) ve bir konum gerekir. Aşağıdaki örnek hello nasıl toocreate bir depolama hizmeti bir konum belirterek gösterir.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

Örnek önceki hello hello hello durumu Not **oluşturma\_depolama\_hesap** işlemi tarafından döndürülen hello sonuç geçirerek alınabilir **oluşturma\_depolama \_hesap** toohello **almak\_işlemi\_durum** yöntemi.  

Depolama hesaplarınızı ve bunların özelliklerini hello ile listeleyebilirsiniz **listesi\_depolama\_hesapları** yöntemi:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"></a>Nasıl yapılır: bir depolama birimi hizmeti Sil
Merhaba depolama hizmeti adı toohello geçirerek bir depolama birimi hizmeti silebilirsiniz **silmek\_depolama\_hesap** yöntemi. Bir depolama birimi hizmeti silme (BLOB'lar, tablolar ve Kuyruklar) hello hizmetinde depolanan tüm verileri siler.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"></a>Nasıl yapılır: listesinde kullanılabilir işletim sistemleri
hizmetlerini barındırmak için kullanılabilir toolist hello işletim sistemleri kullanan hello **listesi\_işletim\_sistemleri** yöntemi:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

Alternatif olarak, hello kullanabilirsiniz **listesi\_işletim\_sistem\_aileleri** hello işletim sistemi ailesi tarafından grupları yöntemi:

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"></a>Nasıl yapılır: bir işletim sistemi görüntüsü oluşturma
tooadd bir işletim sistemi görüntüsü toohello görüntü deposuna kullanmak hello **ekleme\_os\_görüntü** yöntemi:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

kullanılabilir toolist hello işletim sistemi görüntüleri kullanmak hello **listesi\_os\_görüntüleri** yöntemi. Tüm platform görüntüleri ve kullanıcı görüntüleri içerir:

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <a name="DeleteVMImage"></a>Nasıl yapılır: bir işletim sistemi görüntüsünü silme
toodelete kullanıcı görüntüsü kullanmak hello **silmek\_os\_görüntü** yöntemi:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"></a>Nasıl yapılır: bir sanal makine oluşturun
bir sanal makine toocreate, ilk ihtiyacınız toocreate bir [bulut hizmeti](#CreateCloudService).  Hello kullanarak hello sanal makine dağıtımı oluşturmak **oluşturma\_sanal\_makine\_dağıtım** yöntemi:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <a name="DeleteVM"></a>Nasıl yapılır: bir sanal makineyi silme
bir sanal makine toodelete silmeniz hello kullanarak hello dağıtım **silmek\_dağıtım** yöntemi:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

Merhaba bulut hizmeti sonra silinebilir hello kullanarak **silmek\_barındırılan\_hizmet** yöntemi:

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>Nasıl yapılır: bir sanal makine yakalanan görüntüden sanal makine oluşturma
toocapture bir VM görüntüsü, ilk çağırmanız hello **yakalama\_vm\_görüntü** yöntemi:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

İleri toomake hello görüntüsü başarıyla yakalandı, hello kullan emin **listesi\_vm\_görüntüleri** API'sini ve görüntünüzü hello sonuçlarında görüntülenen emin olun:

    images = sms.list_vm_images()

toofinally hello yakalanan görüntüyü kullanarak hello sanal makine oluşturun, hello kullan **oluşturma\_sanal\_makine\_dağıtım** önce ancak bu kez hello vm_image_name yerine geçirirken yöntemi

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

toolearn toocapture bir Linux sanal makine nasıl görürüm hakkında daha fazla bilgi [nasıl tooCapture Linux sanal makine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

toolearn toocapture bir Windows sanal makine nasıl görürüm hakkında daha fazla bilgi [nasıl tooCapture Windows sanal makine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"> </a>Sonraki adımlar
Hizmet Yönetimi hello temellerini öğrendiğinize göre hello erişebilirsiniz [hello Azure Python SDK'sı için tam API başvuru belgeleri](http://azure-sdk-for-python.readthedocs.org/) ve gerçekleştirmek karmaşık görevleri kolayca python uygulamanızı toomanage.

Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
