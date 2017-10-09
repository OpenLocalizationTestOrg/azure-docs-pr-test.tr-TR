<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>Güncelleştirmeler için hazırlama
Tarama ve hello güncelleştirmeyi uygulamak için önce aşağıdaki adımları tooperform hello gerekir:

1. Bir bulut anlık görüntüsünü hello cihaz verileri alın.
2. IP'leri sabit denetleyicinizi yönlendirilebilir ve toohello Internet bağlanabildiğinizden emin olun. Bu IP'ler sabit kullanılan tooservice güncelleştirmeleri tooyour aygıt olacaktır. Bu test cmdlet'i her denetleyicisinde hello Windows PowerShell arabiriminden hello cihaz aşağıdaki hello edebilirsiniz:
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **Örnek çıktı için sabit IP'leri toohello Internet bağlanabildiğinizde Bağlantıyı Sına**

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

Bu el ile ön denetimleri başarıyla tamamladıktan sonra tooscan devam ve hello güncelleştirmeleri yükleyin.

