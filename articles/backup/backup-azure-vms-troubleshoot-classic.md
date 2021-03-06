<properties
    pageTitle="Problembehebung bei der Sicherung von Azure Virtual Machine | Microsoft Azure"
    description="Problembehandlung beim Sichern und Wiederherstellen von Azure VMs"
    services="backup"
    documentationCenter=""
    authors="trinadhk"
    manager="shreeshd"
    editor=""/>

<tags
    ms.service="backup"
    ms.workload="storage-backup-recovery"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="08/26/2016"
    ms.author="trinadhk;jimpark;"/>


# <a name="troubleshoot-azure-virtual-machine-backup"></a>Problembehebung bei der Sicherung von Azure Virtual machine

> [AZURE.SELECTOR]
- [Recovery Services vault](backup-azure-vms-troubleshoot.md)
- [Backup vault](backup-azure-vms-troubleshoot-classic.md)

Behandeln Sie Fehler während Azure Backup mit Informationen in der folgenden Tabelle aufgeführt.

## <a name="discovery"></a>Entdeckung

| Sicherung | Fehlerdetails | Abhilfe |
| -------- | -------- | -------|
| Entdeckung | Fehler beim neuen Artikel - Microsoft Azure Backup gefunden und Fehler. Warten Sie einige Minuten, und versuchen Sie es dann erneut. | Den Erkennungsvorgang nach 15 Minuten erneut.
| Entdeckung | Nicht neue Elemente – wird einem anderen Vorgang bereits ausgeführt. Warten Sie, bis der aktuelle Erkennungsvorgang abgeschlossen wurde. | Keine |

## <a name="register"></a>Registrieren
| Sicherung | Fehlerdetails | Abhilfe |
| -------- | -------- | -------|
| Registrieren | Anzahl der virtuellen Computer angefügten Datenträger überschritt - bitte einige Datenträger auf diesem virtuellen Computer trennen und wiederholen Sie den Vorgang. Azure Backup unterstützt bis zu 16 Daten Datenträgern ein Azure Virtual Machine für Sicherung | Keine |
| Registrieren | Microsoft Azure Backup Fehler interner - warten Sie einige Minuten und versuchen Sie es dann erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an Microsoft Support. | Sie erhalten diese Fehlermeldung aufgrund eines der folgenden nicht unterstützten Konfiguration der VM auf Premium LRS. <br> Premium-Speicher VMs kann mit Recovery Services Depot gesichert werden. [Weitere Informationen](backup-introduction-to-azure-backup.md/#back-up-and-restore-premium-storage-vms) |
| Registrieren | Fehler bei der Registrierung mit Timeout des Vorgangs Agent installieren | Überprüfen Sie, ob die Betriebssystemversion des virtuellen Computers unterstützt wird. |
| Registrieren | Befehl fehlgeschlagen - ist ein anderer Vorgang auf diesen Artikel. Warten Sie, bis der vorherige Vorgang abgeschlossen | Keine |
| Registrieren | Virtuelle Maschinen mit virtuellen Festplatten auf Premium-Speicher gespeichert werden für die Sicherung nicht unterstützt. | Keine |
| Registrieren | VM-Agent ist nicht auf dem virtuellen Computer - erforderliche Voraussetzung, VM-Agent installieren und starten Sie den erneut. | [Mehr](#vm-agent) über VM Agentinstallation und die VM-Agenteninstallation überprüfen. |

## <a name="backup"></a>Sicherung

| Sicherung | Fehlerdetails | Abhilfe |
| -------- | -------- | -------|
| Sicherung | Mit der Snapshot-Status VM Kommunikation. Snapshot VM Sub Vorgang hat das Zeitlimit überschritten. -Finden Sie in der Anleitung zur Fehlerbehebung zur Lösung des Problems. | Dieser Fehler wird ausgelöst, wenn ein mit der VM-Agent Problem oder Netzwerkzugriff auf der Azure-Infrastruktur in irgendeiner Weise blockiert. Weitere Informationen über [Probleme Debuggen von VM-Snapshot](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md). <br> VM-Agent keine Probleme verursacht, starten Sie den virtuellen Computer. Manchmal kann ein falscher Status VM Probleme und die VM neu zurückgesetzt dieses "schlechte" |
| Sicherung | Fehler bei der Sicherung mit interner Fehler - wiederholen Sie den Vorgang in einigen Minuten. Wenn das Problem weiterhin besteht, wenden Sie sich an den Microsoft-Support | Überprüfen Sie, ob es Zugriff auf VM-Speicher ist ein vorübergehendes Problem. [Azure-Status](https://azure.microsoft.com/en-us/status/) , um festzustellen, ob alle laufenden Thema Compute/Speicher-/Netzwerk im Bereich überprüfen. Wiederholung backup Post Problem wird Sie verringert. |
| Sicherung | Den Vorgang konnte nicht ausgeführt werden, wie VM nicht mehr vorhanden ist. | Sicherung kann nicht ausgeführt werden, die VM konfiguriert für Sicherung gelöscht wurde. Beenden Sie weitere Backups auf geschützte Elemente anzeigen, wählen Sie geschützt, und klicken Sie auf Schutz aufheben. Sie können Daten aufbewahren Datenoption Sicherung beibehalten. Sie können Schutz später fortsetzen, für diesen virtuellen Computer auf Konfigurieren im Schutz von registrierten Elemente anzeigen|
| Sicherung | Fehler beim Installieren von Azure Recovery Services ist auf das ausgewählte Element - VM-Agent Voraussetzung für Azure Recovery Services-Erweiterung. Installieren Sie Azure VM-Agent, und starten Sie die Registrierung erneut | <ol> <li>Überprüfen Sie, ob der VM-Agent ordnungsgemäß installiert wurde. <li>Sicherstellen Sie, dass das Flag für die VM-Konfiguration ordnungsgemäß festgelegt ist.</ol> [Mehr](#validating-vm-agent-installation) über VM Agentinstallation und die VM-Agenteninstallation überprüfen. |
| Sicherung | Befehl fehlgeschlagen - ist ein anderer Vorgang derzeit auf diesen Artikel. Warten Sie, bis der vorherige Arbeitsgang beendet ist, und wiederholen | Eine vorhandene Sicherung oder ein Wiederherstellungsauftrag für den virtuellen Computer ausgeführt, und ein neuer Auftrag kann nicht gestartet werden, während der vorhandene Auftrag ausgeführt wird. |
| Sicherung | Erweiterung Installation ist fehlgeschlagen mit dem Fehler "COM+ konnte keine Kommunikation mit dem Microsoft Distributed Transaction Coordinator | Dies bedeutet normalerweise, dass COM+-Dienst nicht ausgeführt wird. Hilfe zu diesem Problem erhalten Sie bei Microsoft Support. |
| Sicherung | Snapshot-Vorgang fehlgeschlagen die VSS-Vorgang "dieses Laufwerk durch BitLocker Drive Encryption gesperrt ist. Dieses Bedienfeld Laufwerk entsperren. | Schalten Sie BitLocker für alle Laufwerke auf dem virtuellen Computer und beobachten Sie die VSS-Problems |
| Sicherung | Virtuelle Maschinen mit virtuellen Festplatten auf Premium-Speicher gespeichert werden für die Sicherung nicht unterstützt. | Keine |
| Sicherung | Azure Virtual Machine wurde nicht gefunden. | Dies geschieht, wenn die primäre VM gelöscht, aber die Sicherungsrichtlinie weiterhin für eine VM Sicherung durchführen. Um diesen Fehler zu beheben: <ol><li>Erstellen Sie den virtuellen Computer mit demselben Namen und derselben Gruppe Ressourcenname [Cloud Service Name], <br>(ODER) <li> Deaktivieren Sie Schutz für diese VM, sodass nachfolgende Backups nicht ausgelöst werden. </ol> |
| Sicherung | VM-Agent ist nicht auf dem virtuellen Computer - erforderliche Voraussetzung, VM-Agent installieren und starten Sie den erneut. | [Mehr](#vm-agent) über VM Agentinstallation und die VM-Agenteninstallation überprüfen. |

## <a name="jobs"></a>Aufträge
| Vorgang | Fehlerdetails | Abhilfe |
| -------- | -------- | -------|
| Auftrag abbrechen | Abbruch wird nicht für diesen Einzelvorgangstyp - warten Sie, bis der Auftrag abgeschlossen ist. | Keine |
| Auftrag abbrechen | Der Auftrag ist nicht in einem abbrechbaren Status - Warten Sie, bis der Auftrag abgeschlossen ist. <br>ODER<br> Der ausgewählte Einzelvorgang nicht abbrechbaren Status - Warten Auftrag abgeschlossen.| Wahrscheinlich ist die fast abgeschlossen; Warten Sie, bis der Auftrag abgeschlossen ist |
| Auftrag abbrechen | Abbrechen des Auftrags nicht möglich, wird nicht ausgeführt-Abbruch werden nur für Aufträge in Bearbeitung sind. Stornieren Sie versuchen auf in Bearbeitung befindlichen Auftrag. | Dies geschieht durch einen vorübergehenden Zustand. Warten Sie eine Minute, und wiederholen Sie den Vorgang abbrechen |
| Auftrag abbrechen | Fehler beim Abbrechen - warten Sie, bis der Auftrag abgeschlossen ist. | Keine |


## <a name="restore"></a>Wiederherstellen
| Vorgang | Fehlerdetails | Abhilfe |
| -------- | -------- | -------|
| Wiederherstellen | Cloud-interner Fehler wiederherstellen | <ol><li>Cloud ist, Wiederherstellen versuchen, mit DNS konfiguriert. Überprüfen Sie <br>$deployment = "ServiceName" Get-AzureDeployment - ServiceName-Steckplatz "Produktion" Get-AzureDns - DnsSettings $deployment. DnsSettings<br>Wenn Adresse konfiguriert ist, bedeutet dies, dass DNS-Einstellungen.<br> <li>Cloud-Dienst, die Sie wiederherstellen möchten, mit reservierte IP-Adressen konfiguriert ist und vorhandene VMs in der Cloud-Dienst in Zustand.<br>Sie können ein Cloud-Dienst IP reserviert wurde, mit folgendem Powershell-Cmdlets überprüfen:<br>$deployment = "Servicename" Get-AzureDeployment - ServiceName-Steckplatz "Produktion" $ab ReservedIPName <br><li>Sie versuchen, einen virtuellen Computer mit folgenden besonderen Netzwerkkonfigurationen in demselben Clouddienst wiederherzustellen. <br>-Virtuelle Maschinen unter Load Balancer-Konfiguration (intern und extern)<br>-Virtuelle Maschinen mit mehreren reserviert<br>-Virtuelle Maschinen mit mehreren NICs<br>Wählen Sie einen neuen Clouddienst in der Benutzeroberfläche oder Siehe [Wiederherstellen Aspekte](./backup-azure-restore-vms.md/#restoring-vms-with-special-network-configurations) für VMs mit speziellen Konfigurationen</ol> |
| Wiederherstellen | Der ausgewählte DNS-Name bereits - Geben Sie einen anderen DNS-Namen und wiederholen. | Der DNS-Name Hier bezieht sich auf den Namen Cloud (normalerweise. cloudapp.net). Dies muss eindeutig sein. Wenn dieser Fehler auftritt, müssen Sie einen anderen VM-Namen während der Wiederherstellung auswählen. <br><br> Dieser Fehler wird nur für Benutzer von Azure-Portal angezeigt. Die Wiederherstellung über PowerShell ist erfolgreich, weil nur die Datenträger wiederhergestellt und die VM erstellt. Der Fehler wird beim Erstellen die VM explizit durch Sie nach Wiederherstellung die Festplatte konfrontiert. |
| Wiederherstellen | Angegebenen virtuellen Netzwerkkonfiguration stimmt nicht - Bitte geben Sie eine andere virtuelle Netzwerkkonfiguration und versuchen Sie es erneut. | Keine |
| Wiederherstellen | Angegebene Cloud-Dienst ist eine reservierte IP-Adresse, die nicht übereinstimmen mit der Konfiguration des virtuellen Computers wird wiederhergestellt - Geben Sie einen andere Cloud-Dienst mit nicht reservierten IP-Adresse, oder wählen Sie einen anderen Wiederherstellungspunkt Wiederherstellen von verwendet. | Keine |
| Wiederherstellen | Cloud-Dienst erreicht maximale Anzahl input Endpunkte - versuchen Sie einen andere Cloud-Dienst oder einen vorhandenen Endpunkt verwenden. | Keine |
| Wiederherstellen | Backup Depot und Ziel Speicherkonto in zwei unterschiedlichen Regionen - sicherstellen, dass das Speicherkonto Wiederherstellungsvorgang angegeben derselben Azure-Region als backup-Depot. | Keine |
| Wiederherstellen | Storage Konto für die Wiederherstellung nicht unterstützt - Basic/Standard Speicherkonten mit lokal redundant oder redundante Replikationseigenschaften Geo unterstützt. Bitte wählen Sie einen unterstützten Speicherkonto | Keine |
| Wiederherstellen | Speicher für Wiederherstellung angegebene Konto ist nicht online - sicher, dass das Speicherkonto Wiederherstellungsvorgang angegeben online | Dies kann durch einen vorübergehenden Fehler in Azure Storage oder aufgrund eines Ausfalls auftreten. Wählen Sie ein anderes Speicherkonto. |
| Wiederherstellen | Ressourcengruppe Kontingent erreicht - einige Ressourcengruppen von Azure-Portal löschen oder Azure wenden, um die Grenzwerte zu erhöhen. | Keine |
| Wiederherstellen | Ausgewählten Subnet existiert nicht - Bitte wählen Sie ein Subnetz existiert | Keine |


## <a name="policy"></a>Richtlinie
| Vorgang | Fehlerdetails | Abhilfe |
| -------- | -------- | -------|
| Richtlinie erstellen | Fehler beim Erstellen der Richtlinie - Aufbewahrung Auswahlmöglichkeiten Richtlinienkonfiguration weiterhin reduzieren. | Keine |


## <a name="vm-agent"></a>VM-Agent

### <a name="setting-up-the-vm-agent"></a>VM-Agent einrichten
In der Regel ist der VM-Agent bereits in VMs aus dem Azure-Katalog erstellt werden. Virtuelle Computer, die von lokalen Rechenzentren migriert werden müssen, nicht der VM-Agent installiert. VM-Agent muss für diese VMs explizit installiert werden. Weitere Informationen zur [Installation des Agenten VM auf einen vorhandenen virtuellen Computer](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

Für Windows-VMs:

- Downloaden Sie und installieren Sie den [Agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Sie benötigen Administratorrechte, um die Installation abzuschließen.
- [Aktualisieren Sie die VM-Eigenschaft](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) an, dass der Agent installiert ist.

Für Linux-VMs:

- Installieren Sie aktuelle [Linux-Agent](https://github.com/Azure/WALinuxAgent) von Github.
- [Aktualisieren Sie die VM-Eigenschaft](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) an, dass der Agent installiert ist.


### <a name="updating-the-vm-agent"></a>VM-Agent aktualisieren
Für Windows-VMs:

- Aktualisieren der VM-Agent ist so einfach wie die [VM-Agent Binärdateien](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)installieren. Sie müssen jedoch sicherstellen, dass kein Sicherungsvorgang ausgeführt wird, während die VM-Agent aktualisiert wird.

Für Linux-VMs:

- Gehen Sie [Linux VM-Agent aktualisieren](../virtual-machines/virtual-machines-linux-update-agent.md).


### <a name="validating-vm-agent-installation"></a>VM-Agent Installation wird überprüft.
Wie Sie für die VM-Agent-Version auf Windows-VMs:

1. Melden Sie sich bei Azure Virtual Machine und navigieren Sie zum Ordner *C:\WindowsAzure\Packages*. Finden Sie die Datei WaAppAgent.exe.
2. Maustaste auf die Datei, **Eigenschaften Sie**und wählen Sie die Registerkarte **Details** . Das Feld Produktversion sollte 2.6.1198.718 oder höher





