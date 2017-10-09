Azure VPN ağ geçidi SKU'ları aşağıdaki hello sunar:

|**SKU**   | **S2S/VNet-VNet<br>Tünelleri** | **P2S<br>Bağlantıları** | **Toplam<br>Aktarım Hızı Kıyaslaması** |
|---       | ---                             | ---                    | ---                         |
|**VpnGw1**| En çok, 30                         | En çok, 128               | 650 Mbps                    |
|**VpnGw2**| En çok, 30                         | En çok, 128               | 1 Gbps                      |
|**VpnGw3**| En çok, 30                         | En çok, 128               | 1,25 Gb/sn                   |
|**Temel** | En çok, 10                         | En çok, 128               | 100 Mbps                    | 
|          |                                 |                        |                             | 

- Toplam Aktarım Hızı Kıyaslaması, tek bir ağ geçidi üzerinde yer alan birden fazla tünelin ölçümlerine bağlıdır. Son tooInternet trafiği koşulları ve uygulama davranışları garantili verimlilik değil.

- Fiyatlandırma bilgileri hello üzerinde bulunabilir [fiyatlandırma](https://azure.microsoft.com/pricing/details/vpn-gateway) sayfası.

- SLA (hizmet düzeyi sözleşmesi) bilgileri hello üzerinde bulunabilir [SLA](https://azure.microsoft.com/support/legal/sla/vpn-gateway/) sayfası.
