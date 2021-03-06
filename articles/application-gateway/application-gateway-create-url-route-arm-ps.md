<properties
   pageTitle="Erstellen Sie ein Gateway mit URL Routingregeln | Microsoft Azure"
   description="Diese Seite enthält Informationen zu erstellen, ein Azure Gateway mit URL-routing-Regeln konfigurieren"
   documentationCenter="na"
   services="application-gateway"
   authors="georgewallace"
   manager="jdial"
   editor="tysonn"/>
<tags
   ms.service="application-gateway"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="infrastructure-services"
   ms.date="10/25/2016"
   ms.author="gwallace"/>


# <a name="create-an-application-gateway-using-path-based-routing"></a>Erstellen Sie ein Gateway mit Pfad-basiertem routing 

> [AZURE.SELECTOR]
- [Azure-portal](application-gateway-create-url-route-portal.md)
- [Azure Ressourcenmanager PowerShell](application-gateway-create-url-route-arm-ps.md)

URL-Pfad-basierte routing können Sie basierte auf den URL-Pfad der HTTP-Anforderung Routen zuordnen. Es überprüft, ob eine Route zum Back-End-Pool für die URL-Listen in Application Gateway konfiguriert und definierten Back-End-Pool den Netzwerkverkehr an. Ein URL-basiertem routing wird Saldo Anfragen für verschiedene Inhaltstypen zu anderen Back-End-Server geladen.

URL-basierte routing stellt einen neuen Typ Application Gateway. Application Gateway hat zwei Regeltypen: grundlegende und PathBasedRouting. Grundlegende Regeltyp bietet Round Robin für Back-End-Pools beim PathBasedRouting neben Round-Robin-Verteilung, berücksichtigt Pfad Muster des angeforderten URL beim Back-End-Pool auswählen.

>[AZURE.IMPORTANT] PathPattern: Die Liste der Pfad Muster übereinstimmen. Jede mit beginnen / und nur einen "\*" darf am Ende. Gültige sind Werte /xyz, /xyz* oder /xyz/*. Pfad Matcher zugeführt Zeichenfolge enthält keinen Text nach dem ersten "?" oder "#" und die Zeichen sind nicht zulässig. 

## <a name="scenario"></a>Szenario
Im folgenden Beispiel Application Gateway dient Datenverkehr für contoso.com mit zwei Back-End-Server: Videoserver und Image Server.

Anfragen für http://contoso.com/image* Bild Serverpool (pool1) und http://contoso.com/video weitergeleitet* werden video Serverpool (pool2) weitergeleitet. Ein Standard-Serverpool (pool1) ist aktiviert, wenn keine Pfad-Muster übereinstimmt.

![URL-route](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Bevor Sie beginnen

1. Installieren Sie die neueste Version von Azure PowerShell-Cmdlets mit dem Webplattform-Installer. Sie können herunterladen und Installieren der neuesten Version von **Windows PowerShell** Teil der [Downloadseite](https://azure.microsoft.com/downloads/).
2. Sie erstellen ein virtuelles Netzwerk und Subnetz für Application Gateway. Stellen Sie sicher, dass keine virtuellen Maschinen oder Cloud-Bereitstellungen im Subnetz verwenden. Application Gateway muss sich in einem virtuellen Netzwerksubnetz sein.
3. Back-End-Pool mit Application Gateway hinzugefügten Server bestehen oder ihre Endpunkte haben das virtuelle Netzwerk oder mit einer öffentlichen IP-Adresse/VIP zugewiesen.



## <a name="what-is-required-to-create-an-application-gateway"></a>Was ist ein Gateway erstellen?


- **Back-End-Serverpool:** Die Liste der IP-Adressen der Back-End-Server. IP-Adressen sollten entweder das virtuelle Netzwerk-Subnetz angehören oder sollte eine öffentliche IP-Adresse/VIP.
- **Back-End-pooleinstellungen:** Jeder Pool hat wie Port, Protokoll und cookiebasierte Affinität. Diese sind an einen Pool gebunden und gelten für alle Server innerhalb des Pools.
- **Front-End-Port:** Dieser Port ist der öffentliche Port, der auf dem Anwendungsgateway geöffnet wird. Datenverkehr trifft dieser Anschluss und dann auf einen Back-End-Server umgeleitet wird.
- **Listener:** Der Listener verfügt über einen Front-End-Port ein Protokoll (Http oder Https sind Groß-/Kleinschreibung), und Name des SSL-Zertifikat (sofern offload Konfigurieren von SSL).
- **Regel:** Bindet den Listener Back-End-Serverpool und definiert die Back-End-Serverpool der Datenverkehr weitergeleitet werden soll, einen bestimmten Listener trifft.

## <a name="create-an-application-gateway"></a>Ein Gateway erstellen

Der Unterschied zwischen Azure Classic und Azure-Ressourcen-Manager ist die Reihenfolge, in der erstellt Application Gateway und die Elemente, die konfiguriert werden müssen.

Mit Ressourcen-Manager alle Elemente, ein Gateway individuell konfiguriert und dann zu Gateway Anwendungsressource.


Hier sind die Schritte, die erforderlich sind, um ein Gateway zu erstellen:

1. Erstellen Sie eine Ressourcengruppe für den Ressourcen-Manager.
2. Erstellen Sie ein virtuelles Netzwerk Subnetz und öffentliche IP-Adresse für das Anwendungsgateway.
3. Gateway-Konfiguration Anwendungsobjekt erstellt.
4. Erstellen Sie eine Ressource auf Gateway.

## <a name="create-a-resource-group-for-resource-manager"></a>Erstellen Sie eine Ressourcengruppe für Ressourcenmanager

Stellen Sie sicher, dass Sie die neueste Version von Azure PowerShell verwenden. Mehr steht unter [Verwendung von Windows PowerShell mit Ressourcen-Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Schritt 1

Melden Sie sich bei Azure

    Login-AzureRmAccount

Sie werden aufgefordert, Ihre Anmeldeinformationen authentifizieren.<BR>

### <a name="step-2"></a>Schritt 2

Überprüfen Sie die Abonnements für das Konto.

    Get-AzureRmSubscription

### <a name="step-3"></a>Schritt 3

Auswählen von Azure Abonnements verwenden. <BR>


    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"

### <a name="step-4"></a>Schritt 4

Erstellen Sie eine Ressourcengruppe (überspringen Sie diesen Schritt, wenn Sie eine vorhandene Ressourcengruppe verwenden).

    New-AzureRmResourceGroup -Name appgw-RG -Location "West US"

Alternativ können Sie auch Tags für eine Ressourcengruppe für Application Gateway erstellen:
    
    $resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 

Azure Ressourcen-Manager muss alle Ressourcengruppen einen Speicherort angeben. Dies wird als Standardspeicherort für Ressourcen in dieser Ressourcengruppe verwendet. Stellen Sie sicher, dass alle Befehle ein Gateway Erstellen derselben Ressourcengruppe verwenden.

Im obigen Beispiel haben wir eine Ressourcengruppe namens "Appgw-RG" und "West US" Position.

>[AZURE.NOTE] Benutzerdefinierte Überprüfung für Ihr Anwendungsgateway konfigurieren, finden Sie unter [erstellen ein Gateway mit benutzerdefinierten Prüfpunkte mit PowerShell](application-gateway-create-probe-ps.md). Checken Sie die [Benutzerdefinierte Probes und Überwachung](application-gateway-probe-overview.md) .

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Erstellen Sie ein virtuelles Netzwerk und Subnetz für Application gateway

Im folgenden Beispiel wird veranschaulicht, wie ein virtuelles Netzwerk mit Ressourcen-Manager erstellen.

### <a name="step-1"></a>Schritt 1

Die Subnetz-Variable ein virtuelles Netzwerk erstellt weisen Sie 10.0.0.0/24 Bereich Adresse zu.

    $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24


### <a name="step-2"></a>Schritt 2

Erstellen Sie ein virtuelles Netzwerk mit dem Namen "Appgwvnet" in Ressource Gruppe "Appgw-Rg" Region West USA Subnetz 10.0.0.0/24 mit dem Präfix 10.0.0.0/16.

    $vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet


### <a name="step-3"></a>Schritt 3

Weisen Sie eine Subnetz Variable für die nächsten Schritte schafft ein Gateway.

    $subnet=$vnet.Subnets[0]

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Erstellen Sie eine öffentliche IP-Adresse für die Front-End-Konfiguration

Erstellen einer öffentlichen IP-Ressource in Ressource Gruppe "Appgw-Rg" für die Region West US "publicIP01".

    $publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic

Eine IP-Adresse erhält das Application Gateway beim Starten des Dienstes.

## <a name="create-application-gateway-configuration"></a>Gateway-Konfiguration erstellen

Alle Konfigurationselemente müssen vor dem Erstellen des Anwendung Gateways eingerichtet werden. Die folgenden Schritte erstellen Konfigurationselemente, die für eine Ressource auf Gateway.

### <a name="step-1"></a>Schritt 1

Erstellen einer Application Gateway IP-Konfigurations mit dem Namen "gatewayIP01". Beim Start Application Gateway nimmt eine IP-Adresse aus dem Subnetz konfiguriert und IP-Adressen im Pool Back-End-IP-Netzwerk-Datenverkehr. Denken Sie daran, dass jede Instanz eine IP-Adresse hat.


    $gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet


### <a name="step-2"></a>Schritt 2

Konfigurieren den Back-End-IP-Adresspool mit der Bezeichnung "pool01" und "pool2" mit IP-Adressen "134.170.185.46, 134.170.188.221,134.170.185.50" für "pool1" und "134.170.186.46, 134.170.189.221,134.170.186.50" für "pool2".


    $pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50

    $pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.46, 134.170.189.221,134.170.186.50

In diesem Beispiel sind zwei Back-End-Pools für Netzwerkdatenverkehr anhand der URL-Pfad. Ein Pool empfängt Verkehr von URL-Pfad "/ video" und andere Ihnen empfangen Pfad "/ image". Ersetzen Sie die vorherigen Adressen eigene IP-Adresse Anwendungsendpunkte hinzufügen. 

### <a name="step-3"></a>Schritt 3

Konfigurieren Sie Application Gateway Einstellung "poolsetting01" und "poolsetting02" für den Netzwerkverkehr mit Lastenausgleich im Back-End-Pool. In diesem Beispiel konfigurieren Sie anderen Back-End-Pool für die Back-End-Pools. Jedem Back-End-Pool können eigene Back-End-Pool-Einstellung.

    $poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

    $poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240

### <a name="step-4"></a>Schritt 4

Konfigurieren Sie die Front-End-IP-Adresse mit öffentlichen IP-Endpunkt.

    $fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip

### <a name="step-5"></a>Schritt 5 

Konfigurieren Sie den Front-End-Anschluss für ein Gateway.

    $fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
### <a name="step-6"></a>Schritt 6

Konfigurieren Sie den Listener. Dadurch wird den Listener für die öffentliche IP-Adresse und Port für den Empfang von eingehenden Netzwerkverkehr konfiguriert. 
 
    $listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01

### <a name="step-7"></a>Schritt 7 

Konfigurieren Sie Regel URL-Pfade für die Back-End-Pools. Dieser Schritt konfiguriert den relativen Pfad zur Application Gateway definieren die Zuordnung zwischen URL-Pfad und die Back-End-Pool zugewiesen ist, eingehenden Datenverkehr verarbeitet.

Im folgenden Beispiel werden zwei Regeln erstellt: eine "Image /" Pfad Datenverkehr an eine "Video /" Pfad Datenverkehr an "pool2" Back-End und Back-End "pool1".
    
    $imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

    $videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02

Pfad-Zuordnung Regelkonfiguration konfigurieren auch Standardpool Backend-Adresse bei der Pfad eines vordefinierten Pfadregeln übereinstimmt. 

    $urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02

### <a name="step-8"></a>Schritt 8

Erstellen Sie eine Regel festlegen. Dieser Schritt konfiguriert das Application Gateway URL Path-basiertem routing verwenden.

    $rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap

### <a name="step-9"></a>Schritt 9

Konfigurieren Sie die Anzahl der Instanzen und Größe für das Application Gateway.

    $sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2

## <a name="create-application-gateway"></a>Application Gateway erstellen

Erstellen Sie ein Gateway mit alle Konfigurationsobjekte aus den vorherigen Schritten.

    $appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku

## <a name="get-application-gateway-dns-name"></a>Application Gateway DNS-Namen

Nachdem das Gateway erstellt wurde, besteht der nächste Schritt zum Konfigurieren von front-End für die Kommunikation. Wenn eine öffentliche IP-Adresse verwenden, erfordert Application Gateway einen dynamisch zugewiesenen DNS-Namen nicht ist. Um sicherzustellen, dass Endbenutzer das Application Gateway einen CNAME-Eintrag treffen können auf den öffentlichen Endpunkt Application Gateway verwendet werden. [Einen benutzerdefinierten Domänennamen für in Azure konfigurieren](../cloud-services/cloud-services-custom-domain-name-portal.md). Rufen Sie dazu Details Application Gateway und den zugeordneten IP/DNS-Namen mithilfe des Öffentl.IP-Elements Application Gateway zugeordnet. Application Gateway DNS-Namen zum einen CNAME-Eintrag erstellen, der zwei ASP.NET-Webanwendungen auf dem DNS-Namen verweist. Die Verwendung von A-Datensätze wird nicht empfohlen, da die VIP Neustart des Application Gateway ändern kann.
    
    Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
        
    Name                     : publicIP01
    ResourceGroupName        : appgw-RG
    Location                 : westus
    Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
    Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
    ResourceGuid             : 00000000-0000-0000-0000-000000000000
    ProvisioningState        : Succeeded
    Tags                     : 
    PublicIpAllocationMethod : Dynamic
    IpAddress                : xx.xx.xxx.xx
    PublicIpAddressVersion   : IPv4
    IdleTimeoutInMinutes     : 4
    IpConfiguration          : {
                                 "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                               Configurations/frontend1"
                               }
    DnsSettings              : {
                                 "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                               }

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie Secure Sockets Layer (SSL) Offload erfahren möchten, finden Sie unter [konfigurieren ein Gateway für SSL-Verschiebung](application-gateway-ssl-arm.md).