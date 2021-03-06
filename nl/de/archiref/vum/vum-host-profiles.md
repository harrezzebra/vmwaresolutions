---

copyright:

  years:  2016, 2018

lastupdated: "2018-10-29"

---

#	Hostprofile

vCenter beinhaltet ein Feature 'Hostprofile'. Dieses Feature erstellt ein Profil, das eine vorkonfigurierte und validierte Referenzhostkonfiguration erfasst und einem Systemadministrator hilft, die Hostkonfigurationen in einem Cluster zu verwalten. Hostprofile stellen einen automatisierten und zentral verwalteten Mechanismus für die Hostkonfiguration und die Konfigurationskonformität bereit. Hostprofile ermöglichen es, eine Konfiguration als verwaltetes Objekt zu behandeln, das einen Katalog von Parametern für die Konfiguration enthält: für den Netzbetrieb, den Speicher, die Sicherheit und andere Parameter auf der Hostebene. Diese Hostprofile können auf einzelne Hosts, einen Cluster oder auf alle Hosts und Cluster, die einem Hostprofil zugeordnet sind, angewendet werden.

Wenn mehr VCS vSphere ESXi-Hosts von der IC4VS-Automation bereitgestellt werden, die den ursprünglichen Cluster bereitgestellt hat, gibt es weniger Konfigurationsabweichungen als bei manuellen Methoden zum Hinzufügen von Hosts. Systemadministratoraktionen außerhalb der Automation können die Hostkonfiguration jedoch anders gestalten. Zum Beispiel können mehr NFS-Speicher oder zusätzliche VLANs hinzugefügt werden. Daher ist die Verwendung von Hostprofilen zur Validierung der Konfiguration eines neuen Hosts durch die Überprüfung der Konformität dieses Hosts mit einem vorhandenen Host ein gültiger Anwendungsfall dieses Tools in IBM Cloud.

Informationen zum Hinzufügen weiterer Hosts zu Ihrem vCenter Server-Cluster finden Sie unter [Kapazität für vCenter Server-Instanzen erweitern und verringern](../../vcenter/vc_addingremovingservers.html).

Folgendes ist zu beachten:
*	Bei Instanzen, die in V2.1 oder höher bereitgestellt wurden bzw. für die ein Upgrade auf eine entsprechende Version durchgeführt wurde, werden als Patches für neu bereitgestellte ESXi-Server und Cluster aktuelle, jedoch nicht zwingend die neuesten ESXi-Updates von VMware verwendet.
*	Für alle anderen Updates von VMware-Komponenten sind Sie selbst verantwortlich; in diesem Zusammenhang müssen Sie auch sicherstellen, dass neu bereitgestellte ESXi-Server und Cluster über die notwendigen neuesten Updates verfügen.

Es wird empfohlen, dass ein neuer Host nach dem Hinzufügen zu einem Cluster in den Wartungsmodus versetzt wird, damit er vor dem Hosten der Workloads überprüft und korrigiert werden kann.

Zur Prüfung der Konformität sind die folgenden Schritte in der angegebenen Reihenfolge auszuführen:
1.	Erstellen Sie ein Hostprofil aus einem vorhandenen Host.
2.	Hängen Sie den neuen Host an das Hostprofil an.
3.	Überprüfen Sie die Konformität des neuen Hosts mit dem Hostprofil.
4.	Untersuchen Sie die Konformitätsfehler und beheben Sie sie.

##	Hostprofil aus einem vorhandenen Host erstellen

1.	Klicken Sie in vSphere Web Client' unter 'Home' auf **Richtlinien und Profile**.
2.	Klicken Sie auf **Hostprofile** und navigieren Sie zu der Ansicht 'Hostprofile'.
3.	Klicken Sie auf das Symbol **Profil vom Host extrahieren**.
4.	Wählen Sie einen vorhandenen Host aus, der als Referenzhost dienen soll, und klicken Sie auf **Weiter**.
5.	Geben Sie den Namen und eine Beschreibung für das neue Profil ein und klicken Sie auf **Weiter**.
6.	Überprüfen Sie die Zusammenfassung für das neue Profil und klicken Sie auf **Fertigstellen**.
7.	Das neue Profil wird in der Profilliste angezeigt.

##	Neuen Host an das Hostprofil anhängen

1.	Wählen Sie in der **Profilliste** in der Hauptansicht "Hostprofile" das zuvor erstellte Hostprofil aus, damit es auf den neuen Host angewendet werden kann.
2.	Klicken Sie auf das Symbol zum **Anhängen/Abhängen eines Hostprofils an Hosts und Cluster**.
3.	Wählen Sie den neuen Host aus der erweiterten Liste aus und klicken Sie auf **Zuordnen**.
4.	Der Host wird zur Liste der angehängten Entitäten hinzugefügt.
5.	Klicken Sie auf **Weiter** und dann auf **Fertigstellen**.

##	Konformität des neuen Hosts mit dem Hostprofil überprüfen

1.	Navigieren Sie zu dem Hostprofil, das zuvor erstellt wurde.
2.	Klicken Sie auf das Symbol **Hostprofilübereinstimmung überprüfen**.
3.	Auf der Registerkarte **Objekte** wird der Konformitätsstatus wie folgt aktualisiert: _Übereinstimmung, Unbekannt oder Nicht übereinstimmend_. Der Status 'Nicht übereinstimmend' bedeutet, dass eine Inkonsistenz zwischen dem Profil und dem Host besteht.

##	Konformitätsfehler untersuchen und beheben

1.	Wenn Sie weitere Details zu Konformitätsfehlern anzeigen möchten, wählen Sie das **Hostprofil** auf der Registerkarte **Objekte** aus, das in der Konformitätsprüfung verwendet wird.
2.	Klicken Sie auf die Registerkarte **Überwachen** und wählen Sie die **Konformitätsansicht** aus, um bestimmte Details dazu anzuzeigen, welche Parameter sich zwischen dem nicht konformen Host und dem Hostprofil unterscheiden.
3.	Erweitern Sie die Objekthierarchie und wählen Sie den fehlerhaften Host aus.
4.	Die sich unterscheidenden Parameter werden im Konformitätsfenster unterhalb der Hierarchie angezeigt.
5.	Überprüfen Sie die Parameter und finden Sie heraus, warum sich der neue Host vom Referenzhost unterscheidet. Für Parameter, bei denen die Übereinstimmung nicht akzeptabel ist (z. B. wenn eine Konfigurationsabweichung durch die Systemadministratoraktion verursacht wurde), müssen Sie den Fehler korrigieren, bevor der neue Host aus dem Wartungsmodus versetzt wird.

### Zugehörige Links

* [VMware HCX on IBM Cloud Solution Architecture](https://www.ibm.com/cloud/garage/files/HCX_Architecture_Design.pdf)
* [VMware Solutions on IBM Cloud Digital Technical Engagement](https://ibm-dte.mybluemix.net/ibm-vmware) (Demos)
