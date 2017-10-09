## <a name="application-gateway"></a><span data-ttu-id="97b62-101">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="97b62-101">Application Gateway</span></span>
<span data-ttu-id="97b62-102">Uygulama ağ geçidi bir Azure tarafından yönetilen HTTP yük katman 7 Yük Dengeleme dayalı çözüm Dengelemesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="97b62-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="97b62-103">Uygulama Yük Dengeleme HTTP tabanlı ağ trafiği için yönlendirme kurallarını hello kullanımına izin verir.</span><span class="sxs-lookup"><span data-stu-id="97b62-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="97b62-104">Özellik</span><span class="sxs-lookup"><span data-stu-id="97b62-104">Property</span></span> | <span data-ttu-id="97b62-105">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97b62-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97b62-106">**Backendaddresspool**</span><span class="sxs-lookup"><span data-stu-id="97b62-106">**backendAddressPools**</span></span> |<span data-ttu-id="97b62-107">Merhaba hello arka uç sunucularının IP adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="97b62-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="97b62-108">listede hello IP adresleri ya da toohello sanal ağ alt ait olması gerekir ya da bir genel IP/VIP'ye veya özel IP olmalıdır</span><span class="sxs-lookup"><span data-stu-id="97b62-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="97b62-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="97b62-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="97b62-110">Her bir havuz bağlantı noktası, protokol ve tanımlama bilgisi tabanlı benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="97b62-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="97b62-111">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucuları</span><span class="sxs-lookup"><span data-stu-id="97b62-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="97b62-112">**Frontendport**</span><span class="sxs-lookup"><span data-stu-id="97b62-112">**frontendPorts**</span></span> |<span data-ttu-id="97b62-113">Bu bağlantı noktası hello uygulama ağ geçidinde açılan hello genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="97b62-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="97b62-114">Bu bağlantı noktası trafik İsabetli ve tooone hello arka uç sunucularının alır yeniden yönlendirildi</span><span class="sxs-lookup"><span data-stu-id="97b62-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="97b62-115">**Httplistener**</span><span class="sxs-lookup"><span data-stu-id="97b62-115">**httpListeners**</span></span> |<span data-ttu-id="97b62-116">Dinleyici sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bunlar büyük küçük harfe duyarlı) ve (SSL yük boşaltımı yapılandırılıyorsa) hello SSL sertifika adı</span><span class="sxs-lookup"><span data-stu-id="97b62-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="97b62-117">**Requestroutingrule**</span><span class="sxs-lookup"><span data-stu-id="97b62-117">**requestRoutingRules**</span></span> |<span data-ttu-id="97b62-118">Merhaba kural hello dinleyici ve hello arka uç sunucusu havuzunu bağlar ve hangi arka uç sunucu havuzu hello trafiğini yönlendirilmesi gerektiğini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="97b62-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="97b62-119">Şu anda yalnızca hepsini olarak çalışır</span><span class="sxs-lookup"><span data-stu-id="97b62-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="97b62-120">Bir uygulama ağ geçidi Json şablonunu örneği:</span><span class="sxs-lookup"><span data-stu-id="97b62-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[variables('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[variables('subnetName')]",
                "properties": {
                  "addressPrefix": "[parameters('subnetPrefix')]"
                }
              }
            ]
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="97b62-121">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="97b62-121">Additional resources</span></span>
<span data-ttu-id="97b62-122">Okuma [ uygulama ağ geçidi REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="97b62-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

