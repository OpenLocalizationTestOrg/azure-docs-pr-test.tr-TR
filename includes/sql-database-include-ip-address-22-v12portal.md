
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. İçinde toohello oturum [Azure portal](https://portal.azure.com/) http://portal.azure.com/ adresindeki.
2. Merhaba sol başlığında tıklatın **TÜMÜNE Gözat**. Merhaba **Gözat** dikey penceresi görüntülenir.
3. Kaydırın ve tıklatın **SQL sunucuları**. Merhaba **SQL sunucuları** dikey penceresi görüntülenir.
   
    ![Azure SQL veritabanı sunucunuzun hello Portalı'nda bulunamıyor][b21-FindServerInPortal]
4. Merhaba kolaylık sağlamak için tıklatın önceki hello denetiminde en aza **Gözat** dikey.
5. Merhaba filtre metin kutusuna hello sunucunuzun adını yazmaya başlayın. Satır görüntülenir.
6. Sunucunuz için Hello satıra tıklayın. Sunucunuz için bir dikey pencerede görüntülenir.
7. Sunucu dikey penceresinde **ayarları**. Merhaba **ayarları** dikey penceresi görüntülenir.
8. Tıklatın **Güvenlik Duvarı**. Merhaba **güvenlik duvarı ayarlarını** dikey penceresi görüntülenir.
   
    ![Ayarlar > Güvenlik Duvarı][b31-SettingsFirewallNavig]
9. Tıklatın **istemcisi ekleme IP**. Merhaba ilk metin kutusuna, yeni kural için bir ad yazın.
10. Merhaba düşük ve yüksek türünde IP adresi istediğiniz hello aralığı için değerleri tooenable.
    
    * Kullanışlı toohave hello düşük değer sonu olabilir **.0** ve hello ile yüksek **.255**.
    
    ![Bir IP adresi aralığı tooallow Ekle][b41-AddRange]
11. **Kaydet** düğmesine tıklayın.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
