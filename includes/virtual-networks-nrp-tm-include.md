## <a name="traffic-manager-profile"></a>Trafik Yöneticisi profili
Trafik Yöneticisi ve onun alt uç nokta kaynağının DNS yönlendirme tooendpoints Azure ve Azure dışında etkinleştirin. Bu tür trafik dağıtım yönlendirme ilkesi yöntemler tarafından yönetilir. Trafik Yöneticisi uç noktası durumu toobe izlenen ve uygun şekilde yolu saptırabilir trafiği bir uç nokta hello durumunu temel de sağlar. 

| Özellik | Açıklama |
| --- | --- |
| **trafficRoutingMethod** |Olası değerler şunlardır: *performans*, *Weighted*, ve *önceliği* |
| **dnsConfig** |Hello profili için FQDN |
| **Protokol** |Olası değerler şunlardır: İzleme Protokolü, *HTTP* ve *HTTPS* |
| **Bağlantı Noktası** |bağlantı noktası izlemesi |
| **Path** |izleme yolu |
| **Uç noktaları** |uç nokta kaynaklar için kapsayıcı |

### <a name="endpoint"></a>Uç Nokta
Bir uç nokta Traffic Manager profilinin bir alt kaynaktır. Web uç noktası toowhich kullanıcı trafiğinin hello trafik Yöneticisi profili kaynak yapılandırılmış hello ilkesine dayanarak dağıtılmış veya bir hizmet temsil eder. 

| Özellik | Açıklama |
| --- | --- |
| **Tür** |Merhaba türü hello uç noktasını, olası değerler şunlardır: *Azure uç noktası*, *dış uç noktası*, ve *iç içe geçmiş uç noktası* |
| **uç noktası Targetresourceıd** |bir hizmeti veya web uç noktası genel IP adresi. Bu, bir Azure ya da dış uç noktası olabilir. |
| **Ağırlık** |uç nokta ağırlığı trafiği yönetiminde kullanılan. |
| **Öncelik** |Merhaba uç noktası, kullanılan toodefine bir yük devretme işlemi önceliği |

Trafik Yöneticisi'nin örnek Json biçiminde: 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a>Ek kaynaklar
Okuma [REST API belgeleri trafik Yöneticisi için](https://msdn.microsoft.com/library/azure/mt163664.aspx) daha fazla bilgi için.

