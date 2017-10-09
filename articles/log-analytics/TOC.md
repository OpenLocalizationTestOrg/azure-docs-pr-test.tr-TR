# Genel Bakış
## [Log Analytics nedir?](log-analytics-overview.md)
## [Veri güvenliği](log-analytics-security.md)

# Kullanmaya Başlama
## [Log Analytics’e kaydolma](log-analytics-get-started.md)
## [Erişimi yönetme](log-analytics-manage-access.md)
## [Kullanım verileri](log-analytics-usage.md)
## [Log Analytics SSS](log-analytics-faq.md)
## [Hizmet sağlayıcıları](log-analytics-service-providers.md)

# Nasıl yapılır?
## Veri toplama
### Bağlı kaynaklar
#### [Windows aracıları](log-analytics-windows-agents.md)
#### [Linux aracıları](log-analytics-agent-linux.md)
#### [Azure sanal makineleri](log-analytics-azure-vm-extension.md)
#### [Azure kaynakları](log-analytics-azure-storage.md)
#### [Operations Manager](log-analytics-om-agents.md)
#### [Configuration Manager](log-analytics-sccm.md)
#### [OMS Ağ Geçidi](log-analytics-oms-gateway.md)
### Veri kaynakları
#### [Veri kaynaklarına genel bakış](log-analytics-data-sources.md)
#### [Windows olayları](log-analytics-data-sources-windows-events.md)
#### [Özel JSON verileri](log-analytics-data-sources-json.md)
#### [Toplanan performans verileri](log-analytics-data-sources-collectd.md)
#### [Nagios ve Zabbix uyarıları](log-analytics-data-sources-alerts-nagios-zabbix.md)
#### [Syslog](log-analytics-data-sources-syslog.md)
#### [Performans sayaçları](log-analytics-data-sources-performance-counters.md)
#### [Linux uygulama performansı](log-analytics-data-sources-linux-applications.md)
#### [IIS günlükleri](log-analytics-data-sources-iis-logs.md)
#### [Özel günlükler](log-analytics-data-sources-custom-logs.md)
#### [Özel alanlar](log-analytics-custom-fields.md)

## Verileri sorgulama
### [Günlük aramalarına genel bakış](log-analytics-log-searches.md)
### [Arama başvurusu](log-analytics-search-reference.md)
#### [Normal ifadeler](log-analytics-log-searches-regex.md)
### [Arama sonuçlarına göre işlem yapma](log-analytics-log-search-takeaction.md)
### [Bilgisayar grupları](log-analytics-computer-groups.md)

## Yeni günlük araması
### [Çalışma alanınızı yükseltme](log-analytics-log-search-upgrade.md)
### [SSS](log-analytics-log-search-faq.md)
### [Günlük aramalarına genel bakış](log-analytics-log-search-new.md)
### [Günlük araması portalları](log-analytics-log-search-portals.md)
#### [Merhaba günlük arama portalını kullanın](log-analytics-log-search-log-search-portal.md)
### [Eski dilden geçiş](log-analytics-log-search-transition.md)
### [Akış bağlayıcısı](log-analytics-flow-tutorial.md)

## Verileri çözümleme
### [Panolar](log-analytics-dashboards.md)
### [Görünüm Tasarımcısı](log-analytics-view-designer.md)
### [Power BI](log-analytics-powerbi.md)
## Uyarı oluşturma
### [Uyarıları anlama](log-analytics-alerts.md)
### [Uyarı eylemleri](log-analytics-alerts-actions.md)
### Uyarı kuralları oluşturma
#### [OMS portalı](log-analytics-alerts-creating.md)
#### [REST API](log-analytics-api-alerts.md)
#### [Resource Manager Şablonu](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
### [Web kancası eylem örneği](log-analytics-alerts-webhooks.md)
### [Uyarı Yönetimi çözümü](log-analytics-solution-alert-management.md)
## Çözümleri kullanma
### [Çözümlere genel bakış](log-analytics-add-solutions.md)
### [Hedef çözümler](../operations-management-suite/operations-management-suite-solution-targeting.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [Activity Log Analytics](log-analytics-activity.md)
### [AD Değerlendirmesi](log-analytics-ad-assessment.md)
### [AD Çoğaltma Durumu](log-analytics-ad-replication-status.md)
### [Aracı Durumu](../operations-management-suite/oms-solution-agenthealth.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [Uyarı yönetimi](log-analytics-solution-alert-management.md)
### [Application Insights Bağlayıcısı](log-analytics-app-insights-connector.md)
### [Azure SQL Analizi](log-analytics-azure-sql.md)
### [Azure Web Apps Analytics](log-analytics-azure-web-apps-analytics.md)
### [Kapasite ve performans](log-analytics-capacity.md)
### [Değişiklik İzleme](log-analytics-change-tracking.md)
### [Kapsayıcılar](log-analytics-containers.md)
### [DNS Analizi](log-analytics-dns.md)
### [BT Hizmet Yönetimi Bağlayıcısı](log-analytics-itsmc-overview.md)
#### [BT Hizmet Yönetimi bağlayıcıları](log-analytics-itsmc-connections.md)
### [Anahtar Kasası](log-analytics-azure-key-vault.md)
### Logic Apps B2B İletileri
#### [Logic Apps B2B İletileri çözümü](../logic-apps/logic-apps-track-b2b-messages-omsportal.md?toc=%2fazure%2flog-analytics%2ftoc.json)
#### [Logic Apps B2B özel izleme şeması](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [Kötü Amaçlı Yazılım Değerlendirmesi](log-analytics-malware.md)
### [Ağ Analizi](log-analytics-azure-networking-analytics.md)
### [Ağ Performansı İzleyicisi](log-analytics-network-performance-monitor.md)
### [Office 365](../operations-management-suite/oms-solution-office-365.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [SCOM Değerlendirmesi](log-analytics-scom-assessment.md)
### [Güvenlik Denetimi](../operations-management-suite/oms-security-getting-started.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [PowerShell ile Service Fabric](log-analytics-service-fabric.md)
#### [Azure Resource Manager ile Service Fabric](log-analytics-service-fabric-azure-resource-manager.md)
### [Hizmet Eşlemesi](../operations-management-suite/operations-management-suite-service-map.md?toc=%2fazure%2flog-analytics%2ftoc.json)
### [SQL Değerlendirmesi](log-analytics-sql-assessment.md)
### [Surface Hub](log-analytics-surface-hubs.md)
### [Güncelleştirme yönetimi](../operations-management-suite/oms-solution-update-management.md)
### [VMware](log-analytics-vmware.md)
### Windows Analizi
#### [Güncelleştirme Uyumluluğu](https://technet.microsoft.com/itpro/windows/manage/update-compliance-get-started)
#### [Yükseltme Hazırlığı](https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started)
### [Kablo Verileri](log-analytics-wire-data.md)
## Geliştirme
### [Veri Toplayıcı API’si](log-analytics-data-collector-api.md)
### [PowerShell cmdlet'leri](log-analytics-powershell-workspace-configuration.md)
### [Resource Manager şablonları](log-analytics-template-workspace-configuration.md)
### [Log Arama API’si](log-analytics-log-search-api.md)
#### [Python](log-analytics-log-search-api-python.md)
### [Uyarı API’si](log-analytics-api-alerts.md)

# Başvuru
## [PowerShell](/powershell/module/azurerm.operationalinsights)
## [REST](/rest/api/loganalytics)

# Kaynaklar
## [Azure Yol Haritası](https://azure.microsoft.com/roadmap/)
## [Fiyatlandırma](https://azure.microsoft.com/pricing/details/log-analytics/)
## [Fiyatlandırma hesaplayıcı](https://azure.microsoft.com/pricing/calculator/)
## [Hizmet güncelleştirmeleri](https://azure.microsoft.com/updates/?product=log-analytics)
## [Windows Analizi](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics)
