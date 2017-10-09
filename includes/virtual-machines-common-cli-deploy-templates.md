
* [Azure’da hızlı bir şekilde sanal makine oluşturma](#quick-create-a-vm-in-azure)
* [Azure’da bir sanal makineyi şablondan dağıtma](#deploy-a-vm-in-azure-from-a-template)
* [Özel bir görüntüden sanal makine oluşturma](#create-a-custom-vm-image)
* [Sanal ağ ve yük dengeleyicisi kullanan bir sanal makine dağıtma](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [Kaynak grubunu kaldırma](#remove-a-resource-group)
* [Bir kaynak grubu dağıtımı için Hello günlüklerini göster](#show-the-log-for-a-resource-group-deployment)
* [Bir sanal makine hakkında bilgi görüntüleme](#display-information-about-a-virtual-machine)
* [Tooa Linux tabanlı sanal makineye bağlanmak](#log-on-to-a-linux-based-virtual-machine)
* [Sanal makineyi durdurma](#stop-a-virtual-machine)
* [Sanal makineyi başlatma](#start-a-virtual-machine)
* [Veri diski ekleme](#attach-a-data-disk)

## <a name="getting-ready"></a>Hazırlanma
Hello Azure CLI ile Azure kaynak gruplarını kullanabilmeniz için önce toohave hello sağ Azure CLI Sürüm ve bir Azure hesabı gerekir. Hello Azure CLI yoksa [yüklemek](../articles/cli-install-nodejs.md).

### <a name="update-your-azure-cli-version-too090-or-later"></a>Azure CLI Sürüm too0.9.0 güncelleştirmek veya daha yenisi
Tür `azure --version` toosee yüklü sürüm 0.9.0'dan zaten var olup olmadığını veya sonraki bir sürümü.

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

Aşağıdakilerden birini kullanarak, sürüm 0.9.0'dan değilse veya daha sonra tooupdate ihtiyacınız yerel yükleyicileri hello aracılığıyla veya **npm** yazarak `npm update -g azure-cli`.

Merhaba aşağıdakileri kullanarak Docker kapsayıcısı Azure CLI çalıştırabilirsiniz [Docker görüntü](https://registry.hub.docker.com/u/microsoft/azure-cli/). Docker ana bilgisayardan hello aşağıdaki komutu çalıştırın:

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a>Azure hesabınızı ve aboneliğinizi ayarlama
Henüz bir Azure aboneliğiniz olmamasına rağmen bir MSDN aboneliğiniz varsa [MSDN abone avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilirsiniz. Veya [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.

Şimdi [tooyour Azure hesabı etkileşimli olarak oturum](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) yazarak `azure login` ve etkileşimli oturum açma deneyimi tooyour Azure hesabı için hello ister. 

> [!NOTE]
> Bir iş veya Okul kimlik ve iki faktörlü kimlik doğrulaması etkin sahip değilse, yapabilecekleriniz biliyorsanız **de** kullanmak `azure login -u` hello yanı sıra iş veya Okul kimliği toolog *olmadan* etkileşimli oturum. Bir iş veya Okul kimliği yok, şunları yapabilirsiniz [bir iş veya Okul kimlik kişisel Microsoft hesabınızı oluşturma](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello toolog aynı şekilde.
>
>

Hesabınızın birden fazla aboneliği olabilir. `azure account list` yazarak aboneliklerinizin aşağıdakine benzer bir listesini görüntüleyebilirsiniz:

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

Merhaba aşağıdakileri yazarak hello geçerli Azure aboneliği ayarlayabilirsiniz. Toomanage istediğiniz hello kaynaklara sahip hello abonelik adı veya hello kimliği kullanın.

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a>Toohello Azure CLI kaynak grubu moduna geç
Varsayılan olarak, hello Azure CLI hello Hizmet Yönetimi modunda başlatır (**asm** modu). Tooswitch tooresource Grup modu aşağıdaki hello yazın.

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a>Azure kaynak şablonlarını ve kaynak gruplarını anlama
Çoğu uygulama farklı kaynak türlerinin bir birleşiminden oluşturulur (bir veya daha fazla VM ve depolama hesabı, bir SQL veritabanı, bir sanal ağ ya da içerik teslim ağı gibi). Varsayılan Azure Hizmet Yönetimi API hello ve hello Klasik Azure portalı bu öğeler hizmeti tarafından bir yaklaşım kullanarak gösterilir. Bu yaklaşım toodeploy gerektirir ve hello ayrı ayrı hizmetlerini tek tek yönetme (veya bunu diğer araçları Bul), dağıtım tek bir mantıksal birim olarak değil.

*Azure Resource Manager şablonları*, ancak, toodeploy mümkün kılar ve bildirim temelli bir şekilde bir mantıksal dağıtım birimi olarak farklı bu kaynakları yönetin. İmperatively Azure hangi toodeploy bir komut sonra başka bir belirten, yerine tüm bir JSON dosyası--tüm hello kaynakları ve ilişkili yapılandırma ve dağıtım parametreleri--dağıtımınızda açıklamak ve biri olarak bu kaynakları Azure toodeploy söyleyin Grup.

Ardından hello yönetebilmeniz için Azure CLI kaynak yönetimi komutları kullanarak hello grubun kaynakları genel yaşam döngüsünü:

* Durdurun, başlatın veya hello grubundaki hello kaynakların tümünü bir defada silme.
* Rol tabanlı erişim denetimi (RBAC) kuralları toolock güvenlik izinleri aşağı üzerlerinde uygulayın.
* İşlemleri denetleme.
* Daha iyi izleme için ek meta verilerle kaynakları etiketleme.

Birçok Azure kaynak gruplarını ve bunlar için hello yapabilecekleriniz hakkında daha fazla bilgi edinebilirsiniz [Azure Resource Manager'a genel bakış](../articles/azure-resource-manager/resource-group-overview.md). Şablon yazmak istiyorsanız bkz. [Azure Resource Manager şablonları yazma](../articles/resource-group-authoring-templates.md).

## <a id="quick-create-a-vm-in-azure"></a>Görev: Azure’da hızlı bir şekilde VM oluşturma
Gereksinim duyduğunuz, hangi görüntü bazen bildiğiniz ve, görüntü bir VM'den şimdi gerekir ve çok hello altyapı hakkında önemli değil--olabilir, tootest bir şey temiz bir VM'ye sahip. Ne zaman olan toouse hello istediğiniz `azure vm quick-create` komut ve bir VM ve alt yapısına hello bağımsız değişkenler gerekli toocreate geçirin.

İlk olarak kaynak grubunuzu oluşturun.

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

İkinci olarak, bir görüntü gereklidir. Resmin hello Azure CLI ile toofind bkz [gezinme ve PowerShell ve hello Azure CLI ile Azure sanal makine görüntüleri seçme](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ancak bu makalede popüler görüntülerin kısa bir listesi verilmiştir. Bu hızlı oluşturma işlemi için CoreOS Kararlı görüntüsü kullanılmaktadır.

> [!NOTE]
> ComputeImageVersion için kısaca 'Son' parametresi hem hello şablon dili ve hello Azure CLI hello olarak sağlayabilirsiniz. Bu, tooalways hello son ve düzeltme eki sürümü hello görüntü komut dosyaları veya şablonları toomodify gerek kalmadan kullandığınız olanak tanır. Bu örnek aşağıda gösterilmiştir.
>
>

| PublisherName | Sunduğu | Sku | Sürüm |
|:--- |:--- |:--- |:--- |
| OpenLogic |CentOS |7 |7.0.201503 |
| OpenLogic |CentOS |7.1 |7.1.201504 |
| CoreOS |CoreOS |Beta |647.0.0 |
| CoreOS |CoreOS |Dengeli |633.1.0 |
| MicrosoftDynamicsNAV |DynamicsNAV |2015 |8.0.40459 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2013 |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Standart |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Enterprise |1.0.0 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-DW |12.0.2430 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-OLTP |12.0.2430 |
| Canonical |UbuntuServer |12.04.5-LTS |12.04.201504230 |
| Canonical |UbuntuServer |14.04.2-LTS |14.04.201503090 |
| MicrosoftWindowsServer |WindowsServer |2012-Datacenter |3.0.201503 |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |4.0.201503 |
| MicrosoftWindowsServer |WindowsServer |Windows-Server-Technical-Preview |5.0.201504 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |1.0.141204 |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |4.3.4665 |

Yalnızca hello girerek, VM oluşturma `azure vm quick-create` komut ve hazır hello ister. Şuna benzer şekilde görünecektir:

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

Yeni VM’niz hazırdır.

## <a id="deploy-a-vm-in-azure-from-a-template"></a>Görev: Azure’da şablondan VM dağıtma
Azure CLI hello bir şablon kullanarak bu bölümleri toodeploy yeni bir Azure VM Hello yönergeleri kullanın. Bu şablon, yeni bir sanal ağ ile tek bir alt ağ ve farklı olarak, tek bir sanal makine oluşturur `azure vm quick-create`, tam olarak istediğiniz, toodescribe sağlar ve hatasız yineleyin. Bu şablon aşağıdaki gibidir:

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a>1. adım: hello şablon parametreleri için hello JSON dosyasını inceleyin
Burada, hello şablonunun hello JSON dosyasının hello içeriği bulunmaktadır. (Merhaba şablonu bulunan de [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)

Merhaba Tasarımcısı, çok parametrelerden biri toogive seçilen veya olabilir daha sabit bir şablon oluşturarak yalnızca birkaç toooffer seçilen şekilde şablonları esnektir. Sipariş toocollect hello bilgileri, parametre olarak toopass hello şablonu gerekir (Bu konuda sahip bir şablon satır içi aşağıda) hello şablon dosyasını açın ve hello inceleyin **parametreleri** değerleri.

Bu durumda, hello şablonu için ister:

* Benzersiz bir depolama hesabı adı.
* Merhaba VM için bir yönetici kullanıcı adı.
* Parola.
* Hello world toouse dışında bir etki alanı adı.
* Ubuntu Server sürüm numarası -- ancak yalnızca bir listesini kabul eder.

[Kullanıcı adı ve parola gereksinimleri](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm) hakkında daha fazla bilgi edinin.

Bu değerleri karar verdiğinizde bir grup için hazır toocreate olduğunuz ve Azure aboneliğinize bu şablonu dağıtabilirsiniz.

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a>2. adım: hello şablonu kullanarak hello sanal makine oluşturma
Parametre değerlerinizi hazır olduktan sonra şablonu dağıtımınız için bir kaynak grubu oluşturun ve ardından hello şablonunu dağıtın.

toocreate hello kaynak grubu, türü `azure group create <group name> <location>` istediğiniz hello grup ve toodeploy istediğiniz hello veri merkezi konum hello adı. Bu işlem hızlı bir şekilde yapılır:

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Şimdi toocreate hello dağıtım, çağrı `azure group deployment create` ve geçirin:

* (JSON şablonu tooa yerel dosya yukarıda hello kaydettiyseniz) hello şablon dosyası.
* Bir şablonu (Merhaba dosyasına GitHub ya da başka bir web adresini toopoint istiyorsanız) URI.
* Merhaba kaynak grubu toodeploy istiyor.
* İsteğe bağlı dağıtım adı.

Merhaba JSON dosyasının hello "parametreleri" bölümüne parametrelerinin istendiğinde toosupply hello değerleri olacaktır. Tüm hello parametre değerlerini belirledikten sonra dağıtımınız başlar.

Örnek aşağıda verilmiştir:

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

Tür bilgileri aşağıdaki hello alırsınız:

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <a id="create-a-custom-vm-image"></a>Görev: Özel bir VM görüntüsü oluşturma
Hello temel kullanım şablonlarının yukarıdaki gördünüz, böylece biz benzer yönergeler toocreate özel bir VM Azure belirli .vhd dosyasından aracılığıyla bir şablon kullanarak artık kullanarak Azure CLI hello. Merhaba burada bu şablon bir belirtilen sanal sabit diskten (VHD) tek bir sanal makine oluşturur farktır.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>1. adım: hello şablonu için başlangıç JSON dosyasını inceleyin
Bu bölümde örnek olarak kullanılmıştır hello şablonu için başlangıç JSON dosyası hello içeriğini aşağıda verilmiştir. (Merhaba şablonu bulunan de [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)

Yeniden, varsayılan değerleri olmayan hello parametrelerini tooenter istediğiniz toofind hello değerler gerekir. Merhaba çalıştırdığınızda `azure group deployment create` komutunu hello Azure CLI, bu değerler, tooenter sorar.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a>Adım 2: hello VHD alın
Bunun için bir .vhd dosyasının gerekli olduğu açıktır. Azure’da zaten sahip olduğunuz dosyayı kullanabilir veya bir tane yükleyebilirsiniz.

Bir Windows tabanlı sanal makine için bkz: [oluşturma ve karşıya yükleme Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Linux tabanlı sanal makine için bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a>3. adım: hello şablonu kullanarak hello sanal makine oluşturma
Şimdi hazır toocreate hello .vhd üzerinde dayalı yeni bir sanal makine demektir. Kullanarak, bir grup toodeploy oluşturma `azure group create <location>`:

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Sonra hello kullanarak hello dağıtım oluşturun `--template-uri` seçeneği toocall doğrudan hello şablonunda (veya hello kullanabilirsiniz `--template-file` seçeneği toouse yerel olarak kaydettiğiniz dosya). Merhaba şablonunda belirtilen Varsayılanları olduğundan, yalnızca birkaç için istenir unutmayın. Merhaba şablonu farklı yerlerde dağıtırsanız, bazı adlandırma çakışmaları hello varsayılan değerlerle (oluşturduğunuz özellikle hello DNS adı) ortaya bulabilirsiniz.

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

Çıktı hello aşağıdaki şöyle görünür:

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Görev: Sanal ağ ve dış yük dengeleyici kullanan çok sanal makineli uygulama dağıtma
Bu şablon toocreate iki sanal makine bir yük dengeleyici altındaki sağlar ve bağlantı noktası 80 üzerinde bir Yük Dengeleme kuralı yapılandırın. Bu şablon ayrıca bir depolama hesabı, sanal ağ, genel IP adresi, kullanılabilirlik kümesi ve ağ arabirimleri dağıtır.

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

Bu adımları toodeploy hello GitHub şablonu deposunu Azure PowerShell komutları aracılığıyla bir Resource Manager şablonu kullanarak bir sanal ağ ve bir yük dengeleyici kullanan bir çoklu VM uygulamayı izleyin.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>1. adım: hello şablonu için başlangıç JSON dosyasını inceleyin
Burada, hello şablonunun hello JSON dosyasının hello içeriği bulunmaktadır. Merhaba en son sürüm, isterseniz bunu bulunduktan [şablonları için hello GitHub deposunda](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json). Bu konuda hello kullanır `--template-uri` hello şablonu, ancak anahtar toocall hello de kullanabilir `--template-file` geçiş toopass yerel bir sürüm.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a>2. adım: hello dağıtım hello şablonu kullanarak oluşturma
Kullanarak hello şablonu için bir kaynak grubu oluşturma `azure group create <location>`. Sonra bu kaynak grubuna bir dağıtım kullanarak oluşturun `azure group deployment create` ve hello kaynak grubu geçirme, dağıtım adı geçirme ve varsayılan değerlere sahip değilse hello şablondaki parametreler için hello istemleri yanıtlama.

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Şimdi hello kullan `azure group deployment create` komut ve hello `--template-uri` seçenek toodeploy hello şablonu. Aşağıda gösterildiği gibi sizden istediğinde parametre değerlerini belirtmeye hazır olun.

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

Bu şablon bir Windows Server görüntüsünü dağıtır; ancak herhangi bir Linux görüntüsü ile kolayca değiştirilebilir. Toocreate Docker küme birden çok swarm yöneticilerine istiyorsunuz? [Bunu yapabilirsiniz](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).

## <a id="remove-a-resource-group"></a>Görev: Kaynak grubunu kaldırma
Tooa kaynak grubu yeniden dağıtabilirsiniz, ancak biriyle bittiğinde kullanarak silebilirsiniz unutmayın `azure group delete <group name>`.

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <a id="show-the-log-for-a-resource-group-deployment"></a>Görev: bir kaynak grubu dağıtımı için hello günlük Göster
Şablon oluştururken veya kullanırken bu işlem yaygın olarak yapılır. Merhaba çağrısı toodisplay hello Dağıtımı günlüklerini bir grup için `azure group log show <groupname>`, oldukça biraz neden oldu--veya bir şeyin kaydetmedi anlamak için yararlı olan bilgiler görüntüler. (Dağıtımlarınızla ilgili daha fazla sorun giderme bilgisi ve sorunlar hakkında diğer bilgiler için bkz. [Azure Resource Manager ile yaygın Azure dağıtım hatalarını giderme](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)

tootarget özel hatalar, örneğin, kullandığınız araçlarla **jq** tooquery şeyler biraz daha hassas bir şekilde, tek tek hangi hataları gibi ihtiyacınız toocorrect. Merhaba aşağıdaki örnek kullanır **jq** bir dağıtım oturum için tooparse **lbgroup**, hataları arayanlar.

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
Neyin yanlış gittiğini hızlıca bulabilir, düzeltebilir ve yeniden deneyebilirsiniz. Durumda aşağıdaki hello hello şablon iki VM hello oluşturma hello .vhd üzerinde bir kilit oluşturulan aynı anda. (Biz hello şablonunu değiştiren sonra hello hızlı bir şekilde dağıtıldı.)

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <a id="display-information-about-a-virtual-machine"></a>Görev: Bir sanal makine hakkında bilgi görüntüleme
Hello kullanarak kaynak grubunuzdaki belirli VM'ler hakkındaki bilgileri görebilirsiniz `azure vm show <groupname> <vmname>` komutu. Grubunuzda birden fazla VM varsa, ilk grubundaki toolist hello VM'ler kullanarak gerekebilir `azure vm list <groupname>`.

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

Ardından, myVM1 öğesini arayın:

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> Tooprogrammatically deposu istiyorsanız ve konsol komutlarınızı hello çıktısını işlemek gibi JSON ayrıştırma aracı toouse isteyebilirsiniz  **[jq](https://github.com/stedolan/jq)**  veya  **[jsawk](https://github.com/micha/jsawk)** , ya da hello görev için iyi dil kitaplıkları.
>
>

## <a id="log-on-to-a-linux-based-virtual-machine"></a>Görev: tooa Linux tabanlı sanal makinede oturum açın
Genellikle bağlı toothrough SSH Linux makinelerdir. Daha fazla bilgi için bkz: [nasıl toouse Linux Azure üzerinde SSH](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a id="stop-a-virtual-machine"></a>Görev: VM durdurma
Şu komutu çalıştırın:

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> Bu durumda bu parametre tookeep hello sanal IP (VIP) hello vnet'in kullanın, vnet içinde son VM hello. <br><br> Merhaba kullanırsanız `StayProvisioned` parametresi, hala hello VM için faturalandırılırsınız.
>
>

## <a id="start-a-virtual-machine"></a>Görev: VM başlatma
Şu komutu çalıştırın:

```azurecli
azure vm start <group name> <virtual machine name>
```

## <a id="attach-a-data-disk"></a>Görev: Veri diski ekleme
Ayrıca tooattach yeni bir disk veya bir içeren olup olmadığını toodecide gerekir veri. Yeni bir disk hello komutu hello .vhd dosyası oluşturur ve bunları hello ekler aynı komutu.

Yeni bir disk tooattach bu komutu çalıştırın:

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

Varolan bir veri diski tooattach bu komutu çalıştırın:

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

Ardından Linux normalde yaptığınız gibi toomount hello disk gerekir.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba ile Azure CLI kullanımı çok daha fazla örnekleri için **arm** modu, bkz: [kullanma hello Mac, Linux ve Windows Azure Resource Manager ile Azure CLI](../articles/xplat-cli-azure-resource-manager.md). Azure kaynaklarını ve bunların kavramları hakkında daha fazla toolearn bkz [Azure Resource Manager'a genel bakış](../articles/azure-resource-manager/resource-group-overview.md).

Kullanabileceğiniz diğer şablonlar için bkz. [Azure Hızlı Başlangıç şablonları](https://azure.microsoft.com/documentation/templates/) ve [Şablon kullanan uygulama çerçeveleri](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
