---
title: aaaAzure DevTest Labs SSS | Microsoft Docs
description: "Toocommon Azure DevTest Labs soruları yanıtlar Bul"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>Azure DevTest Labs SSS
Bu makalede Azure DevTest Labs hakkında hello en yaygın sorulara yanıtlar.

**Genel**
## <a name="what-if-my-question-isnt-answered-here"></a>Ne sorumun cevabı burada cevaplanıp değil mi?
Sorunuzun yanıtını burada listelenmiyorsa, biz yanıt bulmanıza yardımcı olmak için bize bildirin.

* Hello bir soru gönderin [Disqus iş parçacığı](#comments) bu SSS hello sonunda ve hello Azure önbelleği ekip ve diğer topluluk üyeleri bu makale hakkında göster.
* tooreach daha geniş bir kitleye hello üzerinde bir soru gönderin [Azure DevTest Labs MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs)ve hello Azure DevTest Labs ekibi ve hello Topluluğu'nun diğer üyeleri göster.
* toomake özellik isteği gönderme istekleri ve fikir toohello [Azure DevTest Labs kullanıcı sesi](https://feedback.azure.com/forums/320373-azure-devtest-labs).

## <a name="why-should-i-use-azure-devtest-labs"></a>Azure DevTest Labs neden kullanmalıyım?
Azure DevTest Labs takım zaman ve para kaydedebilirsiniz. Geliştiriciler, birkaç farklı tabanları kullanarak kendi ortamlar oluşturabilir ve tooquickly dağıtmak ve uygulamaları yapılandırmak yapıları kullanabilirsiniz. Özel resimler ve formülleri kullanarak, sanal makine şablon olarak kaydedilebilir ve kolayca çoğaltılamaz. Ayrıca, labs tooreduce boşa harcanmasına ve bir ekibin ortamlarını laboratuar yöneticileri izin çeşitli yapılandırılabilir ilkeler sunar. Bu ilkeler Otomatik kapatma, maliyet eşik, kullanıcı ve en fazla VM boyutları başına en fazla VMs içerir. Azure DevTest Labs daha ayrıntılı bir açıklaması için hello okuma [genel bakış](devtest-lab-overview.md) veya izleme hello [tanıtım videosunu](/documentation/videos/videos/what-is-azure-devtest-labs).

## <a name="what-does-worry-free-self-service-mean"></a>"Sorunsuz, Self-Servis" ne anlama geliyor?
"Sorunsuz, Self-Servis" geliştiriciler ve sınayıcılar kendi ortamları gerektiği şekilde oluşturun ve yöneticilerin Azure DevTest Labs en aza indirmenize yardımcı olur bilmesinin hello güvenlik boşa harcanmasına ve maliyet kontrol sahip anlamına gelir. Yöneticiler hangi VM boyutları izin verildiğini hello maksimum VM sayısı ve zaman VM'ler başlatıldı ve bilgisayarı kapat belirtebilirsiniz. Azure DevTest Labs de kolay toomonitor maliyetleri ve kümesi uyarıları toostay hello Laboratuvar kaynaklarında nasıl kullanıldığını farkında kolaylaştırır.

## <a name="how-can-i-use-azure-devtest-labs"></a>Azure DevTest Labs nasıl kullanabilir miyim?
Azure DevTest Labs, geliştirme gerektiren veya test ortamları ve tooreproduce istemediğiniz zaman yararlıdır bunları hızlı bir şekilde ve/veya ilkeleri kaydetme maliyetle yönetin.

Burada, müşterilerimizin Azure DevTest Labs için kullandığı bazı senaryolar vardır:

* Tek bir yerde geliştirme ve test ortamları yönetme, ilkeleri tooreduce maliyet ve özel resimler tooshare kullanan hello takımda oluşturur.
* Özel resimler toosave hello disk durumu hello geliştirme aşamaları boyunca kullanarak bir uygulama geliştirme.
* İlişki tooprogress Hello maliyeti izleme.
* Kalite Güvence test etmek için yığın test ortamları oluşturma.
* Yapılar ve formülleri tooeasily kullanarak yapılandırın ve çeşitli ortamlar bir uygulamayı yeniden oluşturun.
* VM'ler hackathons (işbirlikçi geliştirme veya test çalışma) dağıtma ve hello olay sona erdiğinde sonra kolayca bunları sağlamayı kaldırma özelliklerini.

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>Azure DevTest Labs için nasıl faturalandırılır?
Azure DevTest Labs ücretsiz bir hizmettir labs oluşturma ve hello ilkeleri, şablonları ve yapıları yapılandırma boş olduğundan anlamına gelir. Sanal makineler, depolama hesapları ve sanal ağlar gibi Laboratuvar içinde kullanılan Azure kaynaklarını yalnızca hello için ücret ödersiniz. Laboratuvar kaynaklarını hello maliyet ilgili daha fazla bilgi için bilgiyi [Azure DevTest Labs fiyatlandırma](https://azure.microsoft.com/pricing/details/devtest-lab/).


**Güvenlik**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>Azure DevTest Labs hello farklı güvenlik düzeylerini nelerdir?
Güvenlik erişimi belirlenir [Azure rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-built-in-roles.md). toounderstand nasıl çalışır erişmek için onu toounderstand hello farklarını izin, bir rolü ve kapsamı RBAC tarafından tanımlandığı şekilde yardımcı olur.

* **İzni** -izin tanımlanmış erişim tooa belirli bir eylemdir. Örneğin, bir izin okuma erişimi tooall sanal makineler olabilir.
* **Rol** -gruplandırılmış ve tooa kullanıcı atanmış izinleri rolüdür. Örneğin, "abonelik sahibi" bir abonelik içindeki tooall erişimine sahiptir.
* **Kapsam** -Azure kaynak hiyerarşisini başlangıç içinde bir düzey kapsamıdır. Örneğin, bir kapsam bir kaynak grubu veya tek bir laboratuvar veya hello tüm abonelik olabilir.

Azure DevTest Labs Hello kapsamında rolleri toodefine kullanıcı izinlerini iki tür vardır: Laboratuvar sahip ve Laboratuvar kullanıcı.

* **Laboratuvar sahibi** -Laboratuvar sahibi hello erişim tooany kaynakları hello Laboratuvar içinde yok. Bu nedenle, bunlar ilkeleri değiştirmek, okuma ve herhangi bir VM yazma, hello sanal ağı değiştirin ve benzeri.
* **Laboratuvar kullanıcı** - Laboratuvar kullanıcı VM'ler, ilkeleri ve sanal ağlar gibi tüm Laboratuvar kaynaklarını görüntüleyebilir ancak İlkeleri'ni veya diğer kullanıcılar tarafından oluşturulan herhangi bir VM değiştiremez. Azure DevTest Labs özel rollerinde olası toocreate da olduğunda ve bilgi edinebilirsiniz nasıl hello makaledeki toodo [toospecific Laboratuvar ilkeleri kullanıcı izinleri](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Kapsamları hiyerarşik olduğundan, bir kullanıcının belirli bir kapsamda izinleri olduğunda otomatik olarak çevrelenmiş her alt düzey kapsamındaki bu izinler verilir. Abonelik sahibi toohello rolü atanmış bir kullanıcı örneği için daha sonra bunlar tooall kaynaklarına erişim bir abonelikte varsa. Bu kaynaklar, tüm sanal makineler, tüm sanal ağları ve tüm labs içerir. Bu nedenle, abonelik sahibi, Laboratuvar sahibinin hello rolü otomatik olarak devralır. Ancak, hello ters doğru değil. Laboratuvar sahibi hello abonelik düzeyinden daha düşük bir kapsam erişim tooa laboratuvarı sahiptir. Bu nedenle, bir laboratuvar sahibi mümkün toosee sanal makine veya sanal ağlar ya da hello Laboratuvar dışında olan herhangi bir kaynağa değildir.

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>Belirli bir görevin nasıl rol tooallow kullanıcılar tooperform oluşturulsun mu?
Kapsamlı bir makale hakkında nasıl toocreate özel roller ve ata izinleri toothat rol burada bulunabilir. Burada, "DevTest Labs Gelişmiş izin toostart sahiptir ve tüm sanal makineleri hello laboratuarda Durdur kullanıcı" Merhaba rol oluşturur bir komut dosyası örneği verilmiştir:

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**CI/CD tümleştirme ve Otomasyon**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>Azure DevTest Labs my CI/CD araç zinciri ile tümleşik çalışıyor mu?
VSTS kullanıyorsanız, var olan bir [Azure DevTest Labs görevler uzantısı](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) sağlayan sürüm kanal Azure DevTest Labs'de tooautomate. Bu uzantıyı kullanımlarını hello bazıları şunlardır:

* Oluşturma ve bir VM otomatik olarak dağıtma ve hello son yapı Azure dosya kopyalama veya PowerShell VSTS görevler kullanma ile yapılandırma.
* Bir VM hello durumunu tooreproduce hata test sonra yakalama işlemini otomatik olarak daha fazla araştırma için aynı VM hello.
* Merhaba silme hello hello sonunda VM serbest ardışık düzen artık gerekli olmadığında.

Merhaba aşağıdaki blog gönderileri yönerge ve hello VSTS uzantısı kullanma hakkında bilgi sağlar:

* [Azure DevTest Labs – VSTS uzantısı](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [Varolan bir AzureDevTestLab VSTS gelen yeni bir VM dağıtma](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [VSTS yayın yönetimi için sürekli dağıtımlarını tooAzureDevTestLabs kullanma](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

Diğer CI/CD toolchains için tüm hello VSTS görevler uzantısı benzer şekilde elde edilebilir dağıtmayı hello aracılığıyla elde senaryoları daha önce bahsedilen [Azure Resource Manager şablonları](https://aka.ms/dtlquickstarttemplate) kullanarak [ Azure PowerShell cmdlet'leri](../azure-resource-manager/resource-group-template-deploy.md) ve [.NET SDK'ları](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/). Aynı zamanda [DevTest Labs için REST API'leri](http://aka.ms/dtlrestapis) toointegrate, araç zinciri ile.  


**Sanal Makineler**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>Azure DevTest Labs içinde bkz hello Azure Virtual Machines dikey penceresinde belirli VM'ler neden göremiyorum?
Azure DevTest Labs'de VM oluşturulduğunda, izni olduğundan bu VM tooaccess verilir. Mümkün tooview olan, hem hello labs dikey ve hello **sanal makineleri** dikey. Merhaba DevTest Labs roldeki kullanıcılar hello Laboratuvar hello Laboratuvar'ın aracılığıyla oluşturulan tüm sanal makineleri görebilir **tüm sanal makineleri** dikey. Ancak, hello DevTest Labs roldeki kullanıcılar otomatik olarak diğer oluşturmuş olduğunuz okuma erişimi tooVM kaynakları izin verilmez. Bu nedenle, bu VM'lerin hello görüntülenmez **sanal makineleri** dikey.

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>Merhaba özel resimler ve formüller arasındaki fark nedir?
Formül kaydedip yeniden ek ayarlarını yapılandırabileceğiniz bir görüntü iken bir özel bir VHD (sanal sabit disk) görüntüsüdür. Özel görüntü tooquickly istiyorsanız hello ile çeşitli ortamlar oluşturmak tercih edilebilir aynı temel, sabit bir görüntü. Formül, VM hello son BITS, bir sanal ağ/alt ağ veya belirli bir boyuta tooreproduce hello yapılandırmasını istiyorsanız daha iyi olabilir. Daha ayrıntılı bir açıklama için hello makalesine bakın [özel resimler ve DevTest Labs formüller karşılaştırma](devtest-lab-comparing-vm-base-image-types.md).

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>Merhaba birden çok VM nasıl oluşturabilirim aynı anda aynı şablonu?
Merhaba kullanabilirsiniz [VSTS görevler uzantısı](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) veya [bir Azure Resource Manager şablonu oluştur](devtest-lab-add-vm.md#save-azure-resource-manager-template) bir VM oluşturulurken ve [Windows powershell'den hello Azure Resource Manager şablonu dağıtma ](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>My Azure DevTest Labs laboratuara nasıl mevcut Azure Vm'lerimin hareket?
Lütfen varolan VM'ler tooAzure DevTest Labs toocopy hello adımları izleyin:

1. Bu kullanarak, var olan VM hello VHD dosya Kopyala [Windows PowerShell Betiği](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [Merhaba özel görüntü oluşturma](devtest-lab-create-template.md) Azure DevTest Labs Laboratuvarınızı içinde.
3. Özel görüntüsünden hello laboratuarda bir VM oluşturma

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>Birden çok disk toomy VM'ler ekleyebilir miyim?
Birden çok disk tooVMs ekleme desteklenir.  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>My test etmek için bir Windows işletim sistemi görüntüsü toouse istiyorum, t toopurchase bir MSDN aboneliğiniz var mı?
Geliştirme veya Azure'da sınama toouse Windows istemci işletim sistemi görüntülerini (Windows 7 veya üzeri) gerekiyorsa, ardından Evet, aşağıdakilerden birini yapmanız gerekir:

- [Bir MSDN aboneliği satın](https://www.visualstudio.com/products/how-to-buy-vs).
- bir Kurumsal Anlaşma varsa, bir Azure aboneliği ile Merhaba oluşturun [Enterprise geliştirme ve Test teklif](https://azure.microsoft.com/en-us/offers/ms-azr-0148p).

Her bir MSDN teklif için Azure kredisi hello hakkında daha fazla bilgi için bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/).

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>VHD dosyaları toocreate özel görüntü karşıya hello işlemini nasıl otomatikleştirmek?
İki seçenek vardır:

* [Azure AzCopy](../storage/common/storage-use-azcopy.md#blob-upload) kullanılan toocopy bulunabilir veya hello laboratuvarı ile ilişkilendirilen VHD dosyaları toohello depolama hesabı karşıya yükleyin.
* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) , Windows, OSX ve Linux çalıştıran bir tek başına uygulamadır.   

Laboratuvarınızı ile ilişkili toofind hello hedef depolama hesabı şu adımları izleyin:

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **kaynak grupları** hello sol panelindeki.
3. Bulun ve Laboratuvarınızı ile ilişkili hello kaynak grubu seçin.
4. Merhaba üzerinde **genel bakış** dikey penceresinde hello depolama hesapları birini seçin.
5. Seçin **BLOB'lar**.
6. Merhaba listesinde yüklemeleri arayın. Hiçbiri yoksa tooStep #4 dönün ve başka bir depolama hesabı deneyin.
7. Kullanım hello **URL** AzCopy komut, hedef olarak.

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>Tüm hello VM'ler my Laboratuvar silme işleminin hello nasıl otomatik hale getirebilirsiniz?
Ayrıca toodeleting VM'ler Laboratuvarınızı hello Azure Portalı'ndan bir PowerShell Betiği kullanılarak laboratuvarınızda tüm hello VM'ler silebilirsiniz. Hello hello altında hello parametre değerlerini değiştirmek örneğin, aşağıdaki **değerleri toochange** açıklama. Merhaba alabilir `subscriptionId`, `labResourceGroup`, ve `labName` hello Laboratuvar dikey penceresinde hello Azure portal değerleri.

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**Yapıları**
## <a name="what-are-artifacts"></a>Yapıları nelerdir?
Bir VM son BITS veya, geliştirme araçları kullanılan toodeploy olabilir özelleştirilebilir öğeler ürünleridir. Ekli tooyour VM oluşturulurken birkaç basit tıklama ile oldukları ve hello VM sağlandıktan sonra hello yapıları dağıtmak ve VM yapılandırın. Önceden mevcut olan çeşitli yapılar vardır bizim [genel GitHub depo](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts), ancak ayrıca kolayca [kendi yapıları Yazar](devtest-lab-artifact-author.md).


**Laboratuvarı yapılandırması**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu nasıl bir laboratuvar oluşturulsun mu?
Sağladık bir [GitHub deposunu Laboratuvar Azure Resource Manager şablonları](https://aka.ms/dtlquickstarttemplate) olarak dağıtabileceğiniz- ya da sizin labs için özel şablonlar toocreate değiştirin. Bu şablonların her biri olarak toodeploy hello Laboratuvar tıklayabilirsiniz bir bağlantı vardır-kendi Azure aboneliği altında veya hello şablonu özelleştirmek ve [PowerShell veya Azure CLI kullanarak dağıtımı](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>Neden Vm'lerimin rastgele adlar farklı kaynak gruplarında oluşturulur? Yeniden adlandırma veya miyim bu kaynak gruplarını değiştirme?
Kaynak grupları, Azure DevTest Labs toomanage hello kullanıcı izinleri ve erişim toovirtual makineler için sırayla bu şekilde oluşturulur. Merhaba VM tooanother kaynak grubu, istenen adınızla taşıyabilirsiniz, ancak bunun nedenle önerilmez. Daha fazla esneklik bu deneyimi tooallow geliştirmeye çalışıyoruz.   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>Kaç tane labs altında hello oluşturabiliyorum aynı abonelik?
Abonelik başına oluşturulan labs hello sayısı belirli bir sınır yoktur. Ancak, abonelik başına kullanılan hello kaynakları sınırlıdır. Merhaba hakkında bilgi edinebilirsiniz [sınırlarını ve kotaları uygulanan Azure Aboneliklerde](../azure-subscription-service-limits.md) ve [nasıl tooincrease bu sınırları](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-many-vms-can-i-create-per-lab"></a>Kaç VM Laboratuvar oluşturabilirim?
Laboratuvar oluşturulan VM'ler hello sayısı belirli bir sınır yoktur. Ancak, abonelik başına kullanılan hello kaynakları sınırlıdır (örneğin VM çekirdek, genel IP'ler, vs.). Merhaba hakkında bilgi edinebilirsiniz [sınırlarını ve kotaları uygulanan Azure Aboneliklerde](../azure-subscription-service-limits.md) ve [nasıl tooincrease bu sınırları](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>Doğrudan bağlantı toomy Laboratuvar nasıl paylaşmak?
doğrudan bağlantı tooshare tooyour Laboratuvar kullanıcılar, aşağıdaki yordamı hello gerçekleştirebilirsiniz:

1. Hello Azure portal toohello laboratuvarda göz atın.
2. Tarayıcınızdan Hello Laboratuvar URL'sini kopyalayın ve Laboratuvar Kullanıcılarınızla paylaşabilirsiniz.

> [!NOTE]
> Laboratuvar kullanıcılarınız ile dış kullanıcılar ise bir [Microsoft hesabı](#what-is-a-microsoft-account) ve tooyour şirketin Active Directory'si ait değil, sağlanan toohello bağlantı gezinirken bir hata alabilirsiniz. Bir hata alırsanız, bunları adlarının hello sağ üst köşesindeki hello Azure portalı ve select hello dizin hello Laboratuvar hello bulunduğu tooclick istemeniz **Directory** hello menüsünün bölümünde.
>
>

## <a name="what-is-a-microsoft-account"></a>Bir Microsoft hesabı nedir?
Neredeyse Microsoft cihazları ve Hizmetleri ile yaptığınız her şey için kullandığınız bir Microsoft hesabıdır. Bu bir e-posta adresi ve toosign tooSkype, Outlook.com, OneDrive, Windows Phone ve Xbox LIVE – kullanın ve dosya, fotoğraf, kişileri anlama ve ayarları tooany aygıt izleyebilirsiniz parola olur.

> [!NOTE]
> Microsoft hesabı "Windows Live ID" olarak adlandırılan toobe kullanılır.
>
>


**Sorun giderme**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>My yapı VM oluşturma sırasında başarısız oldu. Bunu nasıl giderebilirim?
Çok başvurun[nasıl DevTest Labs de toodiagnose yapı hataları](devtest-lab-troubleshoot-artifact-failure.md) toolearn tooobtain başarısız, yapı nasıl günlüğe kaydeder.

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>Neden değil my sanal varolan ağ düzgün bir şekilde kaydediliyor?
Bir olasılık, sanal ağ adı nokta içeriyor olabilir. Bu nedenle, deneyin kaldırma nokta veya kısa çizgi ile değiştirerek hello ve daha sonra deneyin kaydetme hello sanal ağ yeniden.

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>Bir "ana kaynak bulunamadı" hatası neden PowerShell VM'den sağlamada alıyorum?
Bir kaynak üst tooanother kaynak olduğunda hello üst kaynak hello alt kaynak oluşturmadan önce mevcut olması gerekir. Yoksa, aldığınız bir **ParentResourceNotFound** hata. Merhaba üst kaynakta bir bağımlılık belirtmezseniz hello alt kaynak hello üst önce dağıtılmış olabilir.

Sanal makineleri bir laboratuar ortamında bir kaynak grubu altında alt kaynaklardır. Azure Resource Manager şablonları toodeploy PowerShell aracılığıyla kullandığınızda, hello PowerShell Betiği sağlanan hello kaynak grubu adı hello laboratuvarı hello kaynak grubu adı olmalıdır. Daha fazla bilgi için bkz: [ortak Azure dağıtım hatalarını giderme ](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound).

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>VM dağıtımı başarısız olursa daha fazla hata bilgileri nereden bulabilirim?
VM Dağıtım hataları hello etkinlik günlükleri yakalanır. Laboratuvar VM'ler etkinlik günlükleri hello aracılığıyla bulabilirsiniz **denetim günlüklerini** veya **sanal makine tanılamaları** hello Laboratuvar'in VM dikey penceresinde hello kaynak menüsünde (Merhaba dikey görüntüler hello VM gelenseçtiktensonra**My sanal makineleri** listesi).

Bazı durumlarda, - hello abonelik sınırı hello VM ile oluşturulan bir kaynak için ne zaman aştı gibi Hello VM dağıtımı başlamadan önce hello dağıtım hata oluşur. Hello Laboratuvar düzeyinde hello hata ayrıntıları bu durumda, yakalanır **etkinlik günlükleri** Bul hello hello sonundaki olabilir **yapılandırma ve ilkeleri** ayarlar. Etkinlik kullanma hakkında daha fazla bilgi Azure'da oturum için bkz: [etkinlik günlükleri tooaudit Eylemler kaynaklardaki Görünüm](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
