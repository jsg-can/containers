---

copyright:
  years: 2014, 2018
lastupdated: "2018-01-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Ingress-Annotationen
{: #ingress_annotation}

Um Ihrer Lastausgleichsfunktion für Anwendungen Funktionalität hinzuzufügen, können Sie Annotationen als Metadaten in einer Ingress-Ressource angeben.
{: shortdesc}

Allgemeine Informationen zu Ingress-Services und eine Einführung in deren Verwendung finden Sie in [Öffentlichen Zugriff auf eine App durch Verwenden von Ingress konfigurieren](cs_ingress.html#config).

<table>
<col width="20%">
<col width="20%">
<col width="60%">
 <thead>
 <th>Allgemeine Annotationen</th>
 <th>Name</th>
 <th>Beschreibung</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="#proxy-external-service">Externe Services</a></td>
 <td><code>proxy-external-service</code></td>
 <td>Pfaddefinitionen zu externen Services wie beispielsweise einem in {{site.data.keyword.Bluemix_notm}} gehosteten Service hinzufügen.</td>
 </tr>
 <tr>
 <td><a href="#alb-id">Weiterleitung der privaten Lastausgleichsfunktion für Anwendungen</a></td>
 <td><code>ALB-ID</code></td>
 <td>Eingehende Anforderungen an Ihre Apps mit einer privaten Lastausgleichsfunktion für Anwendungen weiterleiten.</td>
 </tr>
 <tr>
 <td><a href="#rewrite-path">Pfade neu schreiben</a></td>
 <td><code>rewrite-path</code></td>
 <td>Eingehenden Netzverkehr an einen anderen Pfad weiterleiten, den Ihre Back-End-App überwacht.</td>
 </tr>
 <tr>
 <td><a href="#sticky-cookie-services">Sitzungsaffinität mit Cookies</a></td>
 <td><code>sticky-cookie-services</code></td>
 <td>Eingehenden Netzverkehr mithilfe eines permanenten Cookies immer an denselben Upstream-Server weiterleiten.</td>
 </tr>
 <tr>
 <td><a href="#tcp-ports">TCP-Ports</a></td>
 <td><code>tcp-ports</code></td>
 <td>Zugriff auf eine App über einen vom Standard abweichenden TCP-Port.</td>
 </tr>
 </tbody></table>


<table>
<col width="20%">
<col width="20%">
<col width="60%">
 <thead>
 <th>Annotationen für Verbindungen</th>
 <th>Name</th>
 <th>Beschreibung</th>
  </thead>
  <tbody>
  <tr>
  <td><a href="#proxy-connect-timeout">Angepasste Verbindungs- und Lesezeitlimits</a></td>
  <td><code>proxy-connect-timeout</code></td>
  <td>Zeitraum anpassen, über den die Lastausgleichsfunktion für Anwendungen auf das Herstellen einer Verbindung mit bzw. auf das Lesen von Daten aus der Back-End-App warten soll, bis die Back-End-App als nicht verfügbar betrachtet wird.</td>
  </tr>
  <tr>
  <td><a href="#keepalive-requests">Keepalive-Anforderungen</a></td>
  <td><code>keepalive-requests</code></td>
  <td>Maximale Anzahl von Anforderungen konfigurieren, die über eine Keepalive-Verbindung bedient werden können.</td>
  </tr>
  <tr>
  <td><a href="#keepalive-timeout">Keepalive-Zeitlimit</a></td>
  <td><code>keepalive-timeout</code></td>
  <td>Zeitspanne konfigurieren, die eine Keepalive-Verbindung auf dem Server geöffnet bleibt.</td>
  </tr>
  <tr>
  <td><a href="#upstream-keepalive">Keepalive-Verbindungen für Upstream-Server</a></td>
  <td><code>upstream-keepalive</code></td>
  <td>Maximale Anzahl der inaktiven Keepalive-Verbindungen für einen Upstream-Server konfigurieren.</td>
  </tr>
  </tbody></table>


<table>
<col width="20%">
<col width="20%">
<col width="60%">
 <thead>
 <th>Annotationen für Proxypuffer</th>
 <th>Name</th>
 <th>Beschreibung</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="#proxy-buffering">Pufferung von Clientantwortdaten</a></td>
 <td><code>proxy-buffering</code></td>
 <td>Pufferung einer Clientantwort in der Lastausgleichsfunktion für Anwendungen inaktivieren, während die Antwort an den Client gesendet wird.</td>
 </tr>
 <tr>
 <td><a href="#proxy-buffers">Proxy-Puffer</a></td>
 <td><code>proxy-buffers</code></td>
 <td>Anzahl und Größe der Puffer festlegen, mit denen eine Antwort für eine einzelne Verbindung von einem Proxy-Server gelesen wird.</td>
 </tr>
 <tr>
 <td><a href="#proxy-buffer-size">Puffergröße des Proxys</a></td>
 <td><code>proxy-buffer-size</code></td>
 <td>Größe des Puffers festlegen, mit dem der erste Teil der Antwort gelesen wird, die vom Proxy-Server empfangen wird.</td>
 </tr>
 <tr>
 <td><a href="#proxy-busy-buffers-size">Größe belegter Puffer des Proxys</a></td>
 <td><code>proxy-busy-buffers-size</code></td>
 <td>Größe für Proxypuffer festlegen, die belegt sein können.</td>
 </tr>
 </tbody></table>


<table>
<col width="20%">
<col width="20%">
<col width="60%">
<thead>
<th>Annotationen für Anforderungen und Antworten</th>
<th>Name</th>
<th>Beschreibung</th>
</thead>
<tbody>
<tr>
<td><a href="#proxy-add-headers">Zusätzlicher Clientanforderungs- oder -antwortheader</a></td>
<td><code>proxy-add-headers</code></td>
<td>Einer Clientanforderung Headerinformationen hinzufügen, bevor Sie die Anforderung an Ihre Back-End-App weiterleiten, bzw. einer Clientantwort, bevor Sie die Antwort an den Client senden.</td>
</tr>
<tr>
<td><a href="#response-remove-headers">Entfernen des Clientantwortheaders</a></td>
<td><code>response-remove-headers</code></td>
<td>Headerinformationen aus einer Clientantwort entfernen, bevor die Antwort an den Client weitergeleitet wird.</td>
</tr>
<tr>
<td><a href="#client-max-body-size">Angepasste maximale Länge des Clientanforderungshauptteils</a></td>
<td><code>client-max-body-size</code></td>
<td>Länge des Clientanforderungshauptteils anpassen, die an die Lastausgleichsfunktion für Anwendungen gesendet werden darf.</td>
</tr>
</tbody></table>

<table>
<col width="20%">
<col width="20%">
<col width="60%">
<thead>
<th>Annotationen für Servicegrenzwerte</th>
<th>Name</th>
<th>Beschreibung</th>
</thead>
<tbody>
<tr>
<td><a href="#global-rate-limit">Grenzwerte für globale Rate</a></td>
<td><code>global-rate-limit</code></td>
<td>Verarbeitungsrate für Anforderungen und Anzahl der Verbindungen anhand eines definierten Schlüssels für alle Services begrenzen.</td>
</tr>
<tr>
<td><a href="#service-rate-limit">Grenzwerte für Servicerate</a></td>
<td><code>service-rate-limit</code></td>
<td>Verarbeitungsrate für Anforderungen und Anzahl der Verbindungen anhand eines definierten Schlüssels für bestimmte Services begrenzen.</td>
</tr>
</tbody></table>

<table>
<col width="20%">
<col width="20%">
<col width="60%">
<thead>
<th>Annotationen für HTTPS- und TLS/SSL-Authentifizierung</th>
<th>Name</th>
<th>Beschreibung</th>
</thead>
<tbody>
<tr>
<td><a href="#custom-port">Angepasste HTTP- und HTTPS-Ports</a></td>
<td><code>custom-port</code></td>
<td>Standardports für den HTTP-Netzverkehr (Port 80) und den HTTPS-Netzverkehr (Port 443) ändern.</td>
</tr>
<tr>
<td><a href="#redirect-to-https">HTTP-Weiterleitungen an HTTPS</a></td>
<td><code>redirect-to-https</code></td>
<td>Unsichere HTTP-Anforderungen an Ihre Domäne an HTTPS weiterleiten.</td>
</tr>
<tr>
<td><a href="#mutual-auth">Gegenseitige Authentifizierung</a></td>
<td><code>mutual-auth</code></td>
<td>Gegenseitige Authentifizierung für die Lastausgleichsfunktion für Anwendungen konfigurieren.</td>
</tr>
<tr>
<td><a href="#ssl-services">Unterstützung für SSL-Services</a></td>
<td><code>ssl-services</code></td>
<td>Unterstützung für SSL-Services für den Lastausgleich zulassen.</td>
</tr>
</tbody></table>



## Allgemeine Annotationen
{: #general}

### Externe Services (proxy-external-service)
{: #proxy-external-service}

Hinzufügen von Pfaddefinitionen zu externen Services, wie beispielsweise in {{site.data.keyword.Bluemix_notm}} gehosteten Services.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Fügen Sie Pfaddefinitionen zu externen Services hinzu. Verwenden Sie diese Annotation nur dann, wenn Ihre App für einen externen Service, nicht für einen Back-End-Service, betrieben wird. Wenn Sie diese Annotation verwenden, um eine externe Serviceroute zu erstellen, dann werden zusammen mit ihr nur die Annotationen `client-max-body-size`, `proxy-read-timeout`, `proxy-connect-timeout` und `proxy-buffering` unterstützt. Darüber hinaus werden keine weiteren Annotationen zusammen mit `proxy-external-service` unterstützt.
</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: cafe-ingress
  annotations:
    ingress.bluemix.net/proxy-external-service: "path=&lt;mein_pfad&gt; external-svc=https:&lt;externer_service&gt; host=&lt;meine_domäne&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 80
</code></pre>

<table>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
 </thead>
 <tbody>
 <tr>
 <td><code>path</code></td>
 <td>Ersetzen Sie <code>&lt;<em>mein_pfad</em>&gt;</code> durch den Pfad, an dem der externe Service empfangsbereit ist.</td>
 </tr>
 <tr>
 <td><code>external-svc</code></td>
 <td>Ersetzen Sie <code>&lt;<em>externer_service</em>&gt;</code> durch den externen Service, der aufgerufen werden soll. Beispiel: <code>https://&lt;mein_service&gt;.&lt;region&gt;.mybluemix.net</code>.</td>
 </tr>
 <tr>
 <td><code>host</code></td>
 <td>Ersetzen Sie <code>&lt;<em>meine_domäne</em>&gt;</code> durch die Hostdomäne für den externen Service.</td>
 </tr>
 </tbody></table>

 </dd></dl>

<br />



### Weiterleitung der privaten Lastausgleichsfunktion für Anwendungen
{: #alb-id}

Leiten Sie eingehende Anforderungen an Ihre Apps mit einer privaten Lastausgleichsfunktion für Anwendungen weiter.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Wählen Sie statt der öffentlichen eine private Lastausgleichsfunktion für Anwendungen für die Weiterleitung von eingehenden Anforderungen aus.</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/ALB-ID: "&lt;private_ALB-ID&gt;"
spec:
tls:
- hosts:
  - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
- host: meine_domäne
  http:
    paths:
    - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
</thead>
<tbody>
<tr>
<td><code>&lt;private_ALB-ID&gt;</code></td>
<td>Die ID Ihrer privaten Lastausgleichsfunktion für Anwendungen (Application Load Balancer, ALB). Führen Sie <code>bx cs albs --cluster <mein_cluster></code> aus, um nach der ID der privaten Lastausgleichsfunktion für Anwendungen zu suchen.
</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />



### Pfade neu schreiben (rewrite-path)
{: #rewrite-path}

Weiterleitung des eingehenden Netzverkehrs für den Pfad in der Domäne einer Lastausgleichsfunktion für Anwendungen an einen anderen Pfad, an dem die Back-End-Anwendung empfangsbereit ist.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Die Domäne der Ingress-Lastausgleichsfunktion für Anwendungen leitet eingehenden Netzverkehr für <code>mykubecluster.us-south.containers.mybluemix.net/beans</code> an Ihre App weiter. Ihre App überwacht <code>/coffee</code> statt <code>/beans</code>. Zum Weiterleiten des eingehenden Netzverkehrs an Ihre App fügen Sie eine Annotation zum erneuten Schreiben (rewrite) zur Konfigurationsdatei der Ingress-Ressource hinzu. Dadurch wird sichergestellt, dass der an <code>/beans</code> eingehende Netzverkehr mithilfe des Pfads <code>/coffee</code> an Ihre App weitergeleitet wird. Wenn Sie mehrere Services einschließen, verwenden Sie nur ein Semikolon (;) zum Trennen der Services.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/rewrite-path: "serviceName=&lt;mein_service1&gt; rewrite=&lt;zielpfad1&gt;;serviceName=&lt;mein_service2&gt; rewrite=&lt;zielpfad2&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /beans
        backend:
          serviceName: mein_service1
          servicePort: 80
</code></pre>

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
</tr>
<tr>
<td><code>rewrite</code></td>
<td>Ersetzen Sie <code>&lt;<em>zielpfad</em>&gt;</code> durch den Pfad, an dem Ihre App empfangsbereit ist. Der eingehende Netzverkehr in der Domäne der Lastausgleichsfunktion für Anwendungen wird mithilfe dieses Pfads an den Kubernetes-Service weitergeleitet. Die meisten Apps überwachen keinen bestimmten Pfad, sondern verwenden den Rootpfad und einen bestimmten Port. Im vorstehenden Beispiel wurde der Pfad für 'rewrite' als <code>/coffee</code> definiert.</td>
</tr>
</tbody></table>

</dd></dl>

<br />


### Sitzungsaffinität mit Cookies (sticky-cookie-services)
{: #sticky-cookie-services}

Verwendung der permanenten Cookie-Annotation, um der Lastausgleichsfunktion für Anwendungen Sitzungsaffinität hinzuzufügen und eingehenden Netzverkehr immer an denselben Upstream-Server weiterzuleiten.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Um eine hohe Verfügbarkeit zu erreichen, müssen Sie bei einigen Appkonfigurationen unter Umständen mehrere Upstream-Server bereitstellen, die eingehende Clientanforderungen verarbeiten. Wenn ein Client eine Verbindung mit Ihrer Back-End-App herstellt, kann ein Client für die Dauer einer Sitzung bzw. für die Zeit, die für den Abschluss einer Task erforderlich ist, von demselben Upstream-Server bedient werden. Sie können Ihre Lastausgleichsfunktion für Anwendungen so konfigurieren, dass Sitzungsaffinität sichergestellt ist, indem Sie eingehenden Netzverkehr immer an denselben Upstream-Server weiterleiten.

</br></br>
Jeder Client, der eine Verbindung mit Ihrer Back-End-App herstellt, wird durch die Lastausgleichsfunktion für Anwendungen einem der verfügbaren Upstream-Server zugeordnet. Die Lastausgleichsfunktion für Anwendungen erstellt ein Sitzungscookie, das in der App des Clients gespeichert wird und das in die Headerinformationen jeder Anforderung zwischen der Lastausgleichsfunktion für Anwendungen und dem Client eingeschlossen wird. Die Informationen im Cookie stellen sicher, dass alle Anforderungen während der gesamten Sitzung von demselben Upstream-Server verarbeitet werden.

</br></br>
Wenn Sie mehrere Services einschließen, verwenden Sie ein Semikolon (;) zum Trennen der Services.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/sticky-cookie-services: "serviceName=&lt;mein_service1&gt; name=&lt;cookiename1&gt; expires=&lt;ablaufzeit1&gt; path=&lt;cookiepfad1&gt; hash=&lt;hashalgorithmus1&gt;;serviceName=&lt;mein_service2&gt; name=&lt;cookiename2&gt; expires=&lt;ablaufzeit2&gt; path=&lt;cookiepfad2&gt; hash=&lt;hashalgorithmus2&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: &lt;mein_service1&gt;
          servicePort: 8080
      - path: /myapp
        backend:
          serviceName: &lt;mein_service2&gt;
          servicePort: 80</code></pre>

  <table>
  <caption>Erklärung der Komponenten der YAML-Datei</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
  </tr>
  <tr>
  <td><code>name</code></td>
  <td>Ersetzen Sie <code>&lt;<em>cookiename</em>&gt;</code> durch den Namen eines permanenten Cookies, das während einer Sitzung erstellt wird.</td>
  </tr>
  <tr>
  <td><code>expires</code></td>
  <td>Ersetzen Sie <code>&lt;<em>ablaufzeit</em>&gt;</code> durch den Zeitraum in Sekunden (s), Minuten (m) oder Stunden (h), nach dem das permanente Cookie abläuft. Diese Zeit ist unabhängig von der Benutzeraktivität. Nachdem das Cookie abgelaufen ist, wird es durch den Web-Browser des Clients gelöscht und nicht mehr an die Lastausgleichsfunktion für Anwendungen gesendet. Um beispielsweise eine Ablaufzeit von einer Sekunde, einer Minute oder einer Stunde festzulegen, geben Sie <code>1s</code>, <code>1m</code> oder <code>1h</code> ein.</td>
  </tr>
  <tr>
  <td><code>path</code></td>
  <td>Ersetzen Sie <code>&lt;<em>cookiepfad</em>&gt;</code> durch den Pfad, der an die Ingress-Unterdomäne angehängt werden soll und der angibt, für welche Domänen und Unterdomänen das Cookie an die Lastausgleichsfunktion für Anwendungen gesendet wird. Wenn Ihre Ingress-Domäne beispielsweise <code>www.myingress.com</code> ist und Sie das Cookie in jeder Clientanforderung senden möchten, müssen Sie <code>path=/</code> festlegen. Wenn Sie das Cookie nur für <code>www.myingress.com/myapp</code> und alle zugehörigen Unterdomänen senden möchten, müssen Sie <code>path=/myapp</code> festlegen.</td>
  </tr>
  <tr>
  <td><code>hash</code></td>
  <td>Ersetzen Sie <code>&lt;<em>hashalgorithmus</em>&gt;</code> durch den Hashalgorithmus, der die Informationen im Cookie schützt. Nur <code>sha1</code> wird unterstützt. SHA1 erstellt eine Hashsumme auf der Grundlage der Informationen im Cookie und hängt die Hashsumme an das Cookie an. Der Server kann die Informationen im Cookie entschlüsseln und die Datenintegrität bestätigen.</td>
  </tr>
  </tbody></table>

 </dd></dl>

<br />



### TCP-Ports für Lastausgleichsfunktionen für Anwendungen (tcp-ports)
{: #tcp-ports}

Zugriff auf eine App über einen vom Standard abweichenden TC-Port.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Verwenden Sie diese Annotation für eine App, für die eine Arbeitslast für TCP-Datenströme ausgeführt wird.

<p>**Hinweis**: Die Lastausgleichsfunktion für Anwendungen arbeitet im Durchgriffsmodus und leitet den Datenverkehr an Backend-Apps weiter. Die SSL-Terminierung wird in diesem Fall nicht unterstützt.</p>
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/tcp-ports: "serviceName=&lt;mein_service&gt; ingressPort=&lt;ingress-port&gt; [servicePort=&lt;service-port&gt;]"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: &lt;mein_service&gt;
          servicePort: 80</code></pre>

 <table>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, auf den über einen vom Standard abweichenden TCP-Port zugegriffen werden soll.</td>
  </tr>
  <tr>
  <td><code>ingressPort</code></td>
  <td>Ersetzen Sie <code>&lt;<em>ingress-port</em>&gt;</code> durch den TCP-Port, an dem Sie auf Ihre App zugreifen wollen.</td>
  </tr>
  <tr>
  <td><code>servicePort</code></td>
  <td>Dieser Parameter ist optional. Wenn ein Wert bereitgestellt wird, wird der Port durch diesen Wert ersetzt, bevor der Datenverkehr an die Backend-App gesendet wird. Andernfalls entspricht der Port weiterhin dem Ingress-Port.</td>
  </tr>
  </tbody></table>
  </dd>
  </dl>

<br />



## Annotationen für Verbindungen
{: #connection}

### Angepasste Verbindungs- und Lesezeitlimits (proxy-connect-timeout, proxy-read-timeout)
{: #proxy-connect-timeout}

Festlegen eines angepassten Verbindungs- und Lesezeitlimits für die Lastausgleichsfunktion für Anwendungen. Anpassen des Zeitraums, über den die Lastausgleichsfunktion für Anwendungen auf das Herstellen einer Verbindung mit bzw. auf das Lesen von Daten aus der Back-End-App warten soll, bis die Back-End-App als nicht verfügbar betrachtet wird.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Wenn eine Clientanforderung an die Ingress-Lastausgleichsfunktion für Anwendungen gesendet wird, wird von der Lastausgleichsfunktion für Anwendungen eine Verbindung mit der Back-End-App geöffnet. Standardmäßig wartet die Lastausgleichsfunktion für Anwendungen 60 Sekunden auf eine Antwort von einer Back-End-App. Falls die Back-End-App nicht innerhalb von 60 Sekunden antwortet, wird die Verbindungsanforderung abgebrochen und die Back-End-App als nicht verfügbar angenommen.

</br></br>
Nachdem die Lastausgleichsfunktion für Anwendungen mit der Back-End-App verbunden wurde, werden Antwortdaten aus der Back-End-App von der Lastausgleichsfunktion für Anwendungen gelesen. Zwischen zwei Leseoperationen wartet die Lastausgleichsfunktion für Anwendungen maximal 60 Sekunden auf Daten aus der Back-End-App. Falls die Back-End-App innerhalb von 60 Sekunden keine Daten sendet, wird die Verbindung zur Back-End-App gekappt und die App wird als nicht verfügbar angenommen.
</br></br>
Ein Verbindungszeitlimit und Lesezeitlimit von 60 Sekunden ist die Standardeinstellung auf einem Proxy und sollte in der Regel nicht geändert werden.
</br></br>
Falls die Verfügbarkeit Ihrer App nicht durchgehend gewährleistet ist oder Ihre App aufgrund hoher Workloads langsam antwortet, können Sie die Vebindungs- und Lesezeitlimits nach oben korrigieren. Denken Sie daran, dass sich das Erhöhen des Zeitlimits negativ auf die Leistung der Lastausgleichsfunktion für Anwendungen auswirken kann, da die Verbindung mit der Back-End-App geöffnet bleiben muss, bis das Zeitlimit erreicht wurde.
</br></br>
Sie können andererseits das Zeitlimit nach unten korrigieren, um die Leistung der Lastausgleichsfunktion für Anwendungen zu verbessern. Stellen Sie sicher, dass Ihre Back-End-App Anforderungen auch bei höheren Workloads innerhalb des angegebenen Zeitlimits verarbeiten kann.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/proxy-connect-timeout: "&lt;verbindungszeitlimit&gt;s"
   ingress.bluemix.net/proxy-read-timeout: "&lt;lesezeitlimit&gt;s"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;verbindungszeitlimit&gt;</code></td>
 <td>Die Anzahl der Sekunden, die auf die Herstellung einer Verbindung mit der Back-End-App gewartet werden soll. Beispiel: <code>65s</code>. <strong>Hinweis:</strong> Ein Verbindungszeitlimit kann nicht größer als 75 Sekunden sein.</td>
 </tr>
 <tr>
 <td><code>&lt;lesezeitlimit&gt;</code></td>
 <td>Die Anzahl der Sekunden, die auf das Lesen von Daten aus der Back-End-App gewartet werden soll. Beispiel: <code>65s</code>. <strong>Hinweis:</strong> Ein Lesezeitlimit kann nicht größer als 120 Sekunden sein.</td>
 </tr>
 </tbody></table>

 </dd></dl>

<br />



### Keepalive-Anforderungen (keepalive-requests)
{: #keepalive-requests}

Konfiguration der maximalen Anzahl von Anforderungen, die über eine Keepalive-Verbindung bedient werden können.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie die maximale Anzahl von Anforderungen fest, die über eine Keepalive-Verbindung bedient werden können.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/keepalive-requests: "serviceName=&lt;mein_service&gt; requests=&lt;max._anzahl_anforderungen&gt;"
spec:
tls:
- hosts:
  - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
- host: meine_domäne
  http:
    paths:
    - path: /
      backend:
        serviceName: &lt;mein_service&gt;
        servicePort: 8080</code></pre>

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben. Dieser Parameter ist optional. Die Konfiguration wird auf alle Services auf dem Ingress-Host angewendet, es sei denn, es wird ein Service angegeben. Wird der Parameter bereitgestellt, werden die Keepalive-Anforderung für den angegebenen Service festgelegt. Wird der Parameter nicht bereitgestellt, werden die Keepalive-Anforderungen auf der Serverebene der Datei <code>nginx.conf</code> für alle Services festgelegt, für die die Keepalive-Anforderungen nicht konfiguriert sind.</td>
</tr>
<tr>
<td><code>requests</code></td>
<td>Ersetzen Sie <code>&lt;<em>max._anzahl_anforderungen</em>&gt;</code> durch die maximale Anzahl der Anforderungen, die über eine einzige Keepalive-Verbindung bedient werden können.</td>
</tr>
</tbody></table>

</dd>
</dl>

<br />



### Keepalive-Zeitlimit (keepalive-timeout)
{: #keepalive-timeout}

Konfiguration der Zeitspanne, die eine Keepalive-Verbindung serverseitig geöffnet bleibt.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie die Zeitspanne fest, die eine Keepalive-Verbindung auf dem Server geöffnet bleibt.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/keepalive-timeout: "serviceName=&lt;mein_service&gt; timeout=&lt;zeit&gt;s"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
 </thead>
 <tbody>
 <tr>
 <td><code>serviceName</code></td>
 <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben. Dieser Parameter ist optional. Wird der Parameter bereitgestellt, wird das Keepalive-Zeitlimit für den angegebenen Service festgelegt. Wird der Parameter nicht bereitgestellt, wird das Keepalive-Zeitlimit auf der Serverebene der Datei <code>nginx.conf</code> für alle Services festgelegt, für die das Keepalive-Zeitlimit nicht konfiguriert ist.</td>
 </tr>
 <tr>
 <td><code>timeout</code></td>
 <td>Ersetzen Sie <code>&lt;<em>zeit</em>&gt;</code> durch den Zeitraum in Sekunden. Beispiel:<code>timeout=20s</code>. Der Wert null inaktiviert die Keepalive-Verbindungen für den Client.</td>
 </tr>
 </tbody></table>

 </dd>
 </dl>

<br />



### Keepalive-Verbindungen für Upstream-Server (upstream-keepalive)
{: #upstream-keepalive}

Konfiguration der maximalen Anzahl der inaktiven Keepalive-Verbindungen für einen Upstream-Server.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Ändern Sie die maximale Anzahl inaktiver Keepalive-Verbindungen zu einem Upstream-Server für einen angegebenen Service. Der Upstream-Server verfügt standardmäßig über 64 inaktive Keepalive-Verbindungen.
</dd>


 <dt>YAML-Beispiel einer Ingress-Ressource</dt>
 <dd>

 <pre class="codeblock">
 <code>apiVersion: extensions/v1beta1
 kind: Ingress
 metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/upstream-keepalive: "serviceName=&lt;mein_service&gt; keepalive=&lt;max._anzahl_verbindungen&gt;"
 spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

 <table>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
  </tr>
  <tr>
  <td><code>keepalive</code></td>
  <td>Ersetzen Sie <code>&lt;<em>max._anzahl_verbindungen</em>&gt;</code> durch die maximal zulässige Anzahl der inaktiven Keepalive-Verbindungen zum Upstream-Server. Der Standardwert ist <code>64</code>. Bei Angabe des Werts <code>0</code> werden Keepalive-Verbindungen zum Upstream-Server für den angegebenen Service inaktiviert.</td>
  </tr>
  </tbody></table>
  </dd>
  </dl>

<br />



## Annotationen für Proxypuffer
{: #proxy-buffer}


### Pufferung von Clientantwortdaten (proxy-buffering)
{: #proxy-buffering}

Verwendung der 'buffer'-Annotation, um das Speichern von Antwortdaten in der Lastausgleichsfunktion für Anwendungen während des Sendens von Daten an den Client zu inaktivieren.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Die Ingress-Lastausgleichsfunktion für Anwendungen fungiert als Proxy zwischen Ihrer Back-End-App und dem Client-Web-Browser. Wenn eine Antwort von der Back-End-App an den Client gesendet wird, werden die Antwortdaten standardmäßig in der Lastausgleichsfunktion für Anwendungen gepuffert. Die Lastausgleichsfunktion für Anwendungen verarbeitet die Clientantwort als Proxy und beginnt mit dem Senden der Antwort an den Client (in der Geschwindigkeit des Clients). Nachdem alle Daten aus der Back-End-App von der Lastausgleichsfunktion für Anwendungen empfangen wurden, wird die Verbindung zur Back-End-App gekappt. Die Verbindung von der Lastausgleichsfunktion für Anwendungen zum Client bleibt geöffnet, bis der Client alle Daten empfangen hat.

</br></br>
Falls die Pufferung von Antwortdaten in der Lastausgleichsfunktion für Anwendungen inaktiviert ist, werden Daten sofort von der Lastausgleichsfunktion für Anwendungen an den Client gesendet. Der Client muss eingehende Daten in der Geschwindigkeit der Lastausgleichsfunktion für Anwendungen verarbeiten können. Falls der Client zu langsam ist, gehen unter Umständen Daten verloren.
</br></br>
Die Pufferung von Antwortdaten in der Lastausgleichsfunktion für Anwendungen ist standardmäßig aktiviert.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/proxy-buffering: "False"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>
</dd></dl>

<br />



### Proxypuffer (proxy-buffers)
{: #proxy-buffers}

Konfiguration der Anzahl und Größe der Proxypuffer für die Lastausgleichsfunktion für Anwendungen.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie die Anzahl und Größe der Puffer fest, mit denen eine Antwort für eine einzelne Verbindung von einem Proxy-Server gelesen wird. Die Konfiguration wird auf alle Services auf dem Ingress-Host angewendet, es sei denn, es wird ein Service angegeben. Wenn beispielsweise eine Konfiguration wie <code>serviceName=SERVICE number=2 size=1k</code> angegeben wird, wird '1k' auf den Service angewendet. Wenn eine Konfiguration wie <code>number=2 size=1k</code> angegeben wird, wird '1k' auf alle Services auf dem Ingress-Host angewendet.
</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: proxy-ingress
 annotations:
   ingress.bluemix.net/proxy-buffers: "serviceName=&lt;mein_service&gt; number=&lt;anzahl_puffer&gt; size=&lt;größe&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
 </thead>
 <tbody>
 <tr>
 <td><code>serviceName</code></td>
 <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen eines Service, der 'proxy-buffers' anwenden soll.</td>
 </tr>
 <tr>
 <td><code>number</code></td>
 <td>Ersetzen Sie <code>&lt;<em>anzahl_puffer</em>&gt;</code> durch eine Zahl. Beispiel: <em>2</em>.</td>
 </tr>
 <tr>
 <td><code>size</code></td>
 <td>Ersetzen Sie <code>&lt;<em>größe</em>&gt;</code> durch die Größe der einzelnen Puffer in Kilobyte (k oder K). Beispiel: <em>1K</em>.</td>
 </tr>
 </tbody>
 </table>
 </dd></dl>

<br />


### Puffergröße des Proxys (proxy-buffer-size)
{: #proxy-buffer-size}

Konfiguration der Größe des Proxypuffers, der den ersten Teil der Antwort liest.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie die Größe des Puffers fest, mit dem der erste Teil der Antwort gelesen wird, die vom Proxy-Server empfangen wird. Dieser Teil der Antwort enthält normalerweise einen kleinen Antwortheader. Die Konfiguration wird auf alle Services auf dem Ingress-Host angewendet, es sei denn, es wird ein Service angegeben. Wenn beispielsweise eine Konfiguration wie <code>serviceName=SERVICE size=1k</code> angegeben wird, wird '1k' auf den Service angewendet. Wenn eine Konfiguration wie <code>size=1k</code> angegeben wird, wird '1k' auf alle Services auf dem Ingress-Host angewendet.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: proxy-ingress
 annotations:
   ingress.bluemix.net/proxy-buffer-size: "serviceName=&lt;mein_service&gt; size=&lt;größe&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080
 </code></pre>

<table>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
 </thead>
 <tbody>
 <tr>
 <td><code>serviceName</code></td>
 <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen eines Service, der 'proxy-buffers-size' anwenden soll.</td>
 </tr>
 <tr>
 <td><code>size</code></td>
 <td>Ersetzen Sie <code>&lt;<em>größe</em>&gt;</code> durch die Größe der einzelnen Puffer in Kilobyte (k oder K). Beispiel: <em>1K</em>.</td>
 </tr>
 </tbody></table>

 </dd>
 </dl>

<br />



### Größe belegter Puffer des Proxys (proxy-busy-buffers-size)
{: #proxy-busy-buffers-size}

Konfiguration der Größe für Proxy-Puffer, die belegt sein können.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Begrenzen Sie die Größe aller Puffer, die eine Antwort an den Client senden, während die Antwort noch nicht vollständig gelesen wurde. In der Zwischenzeit können die verbleibenden Puffer die Antwort lesen und bei Bedarf einen Teil der Antwort in einer temporären Datei puffern. Die Konfiguration wird auf alle Services auf dem Ingress-Host angewendet, es sei denn, es wird ein Service angegeben. Wenn beispielsweise eine Konfiguration wie <code>serviceName=SERVICE size=1k</code> angegeben wird, wird '1k' auf den Service angewendet. Wenn eine Konfiguration wie <code>size=1k</code> angegeben wird, wird '1k' auf alle Services auf dem Ingress-Host angewendet.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: proxy-ingress
 annotations:
   ingress.bluemix.net/proxy-busy-buffers-size: "serviceName=&lt;servicename&gt; size=&lt;größe&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
       backend:
         serviceName: mein_service
         servicePort: 8080
         </code></pre>

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen eines Service, der 'proxy-busy-buffers-size' anwenden soll.</td>
</tr>
<tr>
<td><code>size</code></td>
<td>Ersetzen Sie <code>&lt;<em>größe</em>&gt;</code> durch die Größe der einzelnen Puffer in Kilobyte (k oder K). Beispiel: <em>1K</em>.</td>
</tr>
</tbody></table>

 </dd>
 </dl>

<br />



## Annotationen für Anforderungen und Antworten
{: #request-response}


### Zusätzlicher Clientanforderungs- oder Clientantwortheader (proxy-add-headers)
{: #proxy-add-headers}

Hinzufügen von zusätzlichen Headerinformationen zu einer Clientanforderung, bevor die Anforderung an die Back-End-App gesendet wird, bzw. zu einer Clientantwort, bevor die Antwort an den Client gesendet wird.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Die Ingress-Lastausgleichsfunktion für Anwendungen fungiert als Proxy zwischen der Client-App und Ihrer Back-End-App. Clientanforderungen, die an die Lastausgleichsfunktion für Anwendungen gesendet werden, werden (als Proxy) verarbeitet und in eine neue Anforderung umgesetzt, die anschließend vom Ingress-Controller an Ihre Back-End-App gesendet wird. Beim Senden einer Anforderung als Proxy werden Headerinformationen entfernt, z. B. der Benutzername, der ursprünglich vom Client gesendet wurde. Falls Ihre Back-End-App diese Informationen erfordert, können Sie die Annotation <strong>ingress.bluemix.net/proxy-add-headers</strong> verwenden, um der Clientanforderung Headerinformationen hinzuzufügen, bevor die Anforderung von der Lastausgleichsfunktion für Anwendungen an Ihre Back-End-App weitergeleitet wird.

</br></br>
Wenn eine Back-End-App eine Antwort an den Client sendet, wird die Antwort von der Lastausgleichsfunktion für Anwendungen als Proxy gesendet, und die HTTP-Header werden aus der Antwort entfernt. Die Client-Web-App benötigt diese Headerinformationen, um die Antwort erfolgreich verarbeiten zu können. Sie können die Annotation <strong>ingress.bluemix.net/response-add-headers</strong> verwenden, um der Clientanforderung Headerinformationen hinzuzufügen, bevor die Anforderung von der Lastausgleichsfunktion für Anwendungen an Ihre Back-End-App weitergeleitet wird.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/proxy-add-headers: |
      serviceName=&lt;mein_service1&gt; {
      &lt;header1&gt; &lt;wert1&gt;;
      &lt;header2&gt; &lt;wert2&gt;;
      }
      serviceName=&lt;mein_service2&gt; {
      &lt;header3&gt; &lt;wert3&gt;;
      }
    ingress.bluemix.net/response-add-headers: |
      serviceName=&lt;mein_service1&gt; {
      "&lt;header1&gt;: &lt;wert1&gt;";
      "&lt;header2&gt;: &lt;wert2&gt;";
      }
      serviceName=&lt;mein_service2&gt; {
      "&lt;header3&gt;: &lt;wert3&gt;";
      }
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: &lt;mein_service1&gt;
          servicePort: 8080
      - path: /myapp
        backend:
          serviceName: &lt;mein_service2&gt;
          servicePort: 80</code></pre>

 <table>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
  </tr>
  <tr>
  <td><code>&lt;header&gt;</code></td>
  <td>Der Schlüssel der Headerinformationen, die der Clientanforderung bzw. der Clientantwort hinzugefügt werden sollen.</td>
  </tr>
  <tr>
  <td><code>&lt;wert&gt;</code></td>
  <td>Der Wert der Headerinformationen, die der Clientanforderung bzw. der Clientantwort hinzugefügt werden sollen.</td>
  </tr>
  </tbody></table>
 </dd></dl>

<br />



### Entfernen des Clientantwortheaders (response-remove-headers)
{: #response-remove-headers}

Entfernen von Headerinformationen, die in der Clientantwort von der Back-End-App eingeschlossen sind, bevor die Antwort an den Client gesendet wird.
 {:shortdesc}

 <dl>
 <dt>Beschreibung</dt>
 <dd>Die Ingress-Lastausgleichsfunktion für Anwendungen fungiert als Proxy zwischen Ihrer Back-End-App und dem Client-Web-Browser. Clientantworten von der Back-End-App, die an die Lastausgleichsfunktion für Anwendungen gesendet werden, werden (als Proxy) verarbeitet und in eine neue Antwort umgesetzt, die anschließend von der Lastausgleichsfunktion für Anwendungen an Ihren Client-Web-Browser gesendet wird. Auch wenn beim Senden einer Antwort als Proxy die HTTP-Headerinformationen entfernt werden, die ursprünglich von der Back-End-App gesendet wurden, entfernt dieser Prozess möglicherweise nicht alle Back-End-App-spezifischen Header. Entfernen Sie Headerinformationen aus einer Clientantwort, bevor die Antwort von der Lastausgleichsfunktion für Anwendungen an den Client-Web-Browser weitergeleitet wird.</dd>
 <dt>YAML-Beispiel einer Ingress-Ressource</dt>
 <dd>
 <pre class="codeblock">
 <code>apiVersion: extensions/v1beta1
 kind: Ingress
 metadata:
   name: myingress
   annotations:
     ingress.bluemix.net/response-remove-headers: |
       serviceName=&lt;mein_service1&gt; {
       "&lt;header1&gt;";
       "&lt;header2&gt;";
       }
       serviceName=&lt;mein_service2&gt; {
       "&lt;header3&gt;";
       }
 spec:
   tls:
   - hosts:
     - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
   - host: meine_domäne
    http:
      paths:
       - path: /
         backend:
           serviceName: &lt;mein_service1&gt;
           servicePort: 8080
       - path: /myapp
         backend:
           serviceName: &lt;mein_service2&gt;
           servicePort: 80</code></pre>

  <table>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
   </thead>
   <tbody>
   <tr>
   <td><code>serviceName</code></td>
   <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
   </tr>
   <tr>
   <td><code>&lt;header&gt;</code></td>
   <td>Der Schlüssel des Headers, der aus der Clientantwort entfernt werden soll.</td>
   </tr>
   </tbody></table>
   </dd></dl>

<br />


### Angepasste maximale Länge des Clientanforderungshauptteils (client-max-body-size)
{: #client-max-body-size}

Anpassen der maximalen Größe des Hauptteils, den der Client als Teil einer Anforderung senden kann.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Um die erwartete Leistung beizubehalten, ist die maximale Größe des Clientanforderungshauptteils auf 1 Megabyte festgelegt. Wenn eine Clientanforderung mit einer das Limit überschreitenden Hauptteilgröße an die Ingress-Lastausgleichsfunktion für Anwendungen gesendet wird und der Client das Unterteilen von Daten nicht zulässt, gibt die Lastausgleichsfunktion für Anwendungen die HTTP-Antwort 413 (Anforderungsentität zu groß) an den Client zurück. Eine Verbindung zwischen dem Client und der Lastausgleichsfunktion für Anwendungen ist erst möglich, wenn der Anforderungshauptteil verkleinert wird. Wenn der Client das Unterteilen in mehrere Blöcke zulässt, werden die Daten in Pakete von 1 Megabyte aufgeteilt und an die die der Lastausgleichsfunktion für Anwendungen gesendet.

</br></br>
Wenn Sie Clientanforderungen mit einer Hauptteilgröße über 1 Megabyte erwarten, können Sie die maximale Größe des Hauptteils erhöhen. Beispiel: Sie möchten, dass Ihr Client große Dateien hochladen kann. Das Erhöhen der maximalen Größe des Anforderungshauptteils kann sich negativ auf die Leistung Ihrer Lastausgleichsfunktion für Anwendungen auswirken, weil die Verbindung mit dem Client geöffnet bleiben muss, bis die Anforderung empfangen wird.
</br></br>
<strong>Hinweis:</strong> Einige Client-Web-Browser können die HTTP-Antwortnachricht 413 nicht ordnungsgemäß anzeigen.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/client-max-body-size: "size=&lt;größe&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;size&gt;</code></td>
 <td>Die maximal zulässige Größe des Hauptteils der Clientantwort. Um sie beispielsweise auf 200 Megabyte festzulegen, definieren Sie <code>200m</code>.  <strong>Hinweis:</strong> Sie können die Größe auf '0' festlegen, um die Prüfung der Größe des Clientanforderungshauptteils zu inaktivieren.</td>
 </tr>
 </tbody></table>

 </dd></dl>

<br />



## Annotationen für Servicegrenzwerte
{: #service-limit}


### Grenzwerte für globale Rate (global-rate-limit)
{: #global-rate-limit}

Begrenzung der Verarbeitungsrate für Anforderungen und Anzahl der Verbindungen anhand eines definierten Schlüssels für alle Services.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Begrenzen Sie für alle Services anhand eines definierten Schlüssels die Verarbeitungsrate für Anforderungen und die Anzahl der Verbindungen, die von einer einzelnen IP-Adresse für alle Pfade der ausgewählten Backend-Systeme kommen.
</dd>


 <dt>YAML-Beispiel einer Ingress-Ressource</dt>
 <dd>

 <pre class="codeblock">
 <code>apiVersion: extensions/v1beta1
 kind: Ingress
 metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/global-rate-limit: "key=&lt;schlüssel&gt; rate=&lt;rate&gt; conn=&lt;anzahl_der_verbindungen&gt;"
 spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

 <table>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
  </thead>
  <tbody>
  <tr>
  <td><code>key</code></td>
  <td>Um einen globalen Grenzwert für eingehenden Anforderungen basierend auf dem Standort des Service festzulegen, verwenden Sie `key=location`. Um einen globalen Grenzwert für eingehenden Anforderungen basierend auf dem Header festzulegen, verwenden Sie `X-USER-ID key==$http_x_user_id`.</td>
  </tr>
  <tr>
  <td><code>rate</code></td>
  <td>Ersetzen Sie <code>&lt;<em>rate</em>&gt;</code> durch die Verarbeitungsrate. Geben Sie einen Wert als Rate pro Sekunde (r/s) oder Rate pro Minute (r/m) an. Beispiel: <code>50r/m</code>.</td>
  </tr>
  <tr>
  <td><code>conn</code></td>
  <td>Ersetzen Sie <code>&lt;<em>anzahl_der_verbindungen</em>&gt;</code> durch die Anzahl der Verbindungen.</td>
  </tr>
  </tbody></table>

  </dd>
  </dl>

<br />



### Grenzwerte für Servicerate (service-rate-limit)
{: #service-rate-limit}

Begrenzung der Verarbeitungsrate für Anforderungen und Anzahl der Verbindungen für bestimmte Services.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Begrenzen Sie für bestimmte Services die Verarbeitungsrate für Anforderungen und die Anzahl der Verbindungen anhand eines definierten Schlüssels, die von einer einzelnen IP-Adresse für alle Pfade der ausgewählten Backend-Systeme kommen.
</dd>


 <dt>YAML-Beispiel einer Ingress-Ressource</dt>
 <dd>

 <pre class="codeblock">
 <code>apiVersion: extensions/v1beta1
 kind: Ingress
 metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/service-rate-limit: "serviceName=&lt;mein_service&gt; key=&lt;schlüssel&gt; rate=&lt;rate&gt; conn=&lt;anzahl_der_verbindungen&gt;"
 spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

 <table>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Service, für den Sie die Verarbeitungsrate begrenzen wollen.</li>
  </tr>
  <tr>
  <td><code>key</code></td>
  <td>Um einen globalen Grenzwert für eingehenden Anforderungen basierend auf dem Standort des Service festzulegen, verwenden Sie `key=location`. Um einen globalen Grenzwert für eingehenden Anforderungen basierend auf dem Header festzulegen, verwenden Sie `X-USER-ID key==$http_x_user_id`.</td>
  </tr>
  <tr>
  <td><code>rate</code></td>
  <td>Ersetzen Sie <code>&lt;<em>rate</em>&gt;</code> durch die Verarbeitungsrate. Um eine Rate pro Sekunde zu definieren, verwenden Sie 'r/s': <code>10r/s</code>. Um eine Rate pro Minute zu definieren, verwenden Sie 'r/m': <code>50r/m</code>.</td>
  </tr>
  <tr>
  <td><code>conn</code></td>
  <td>Ersetzen Sie <code>&lt;<em>anzahl_der_verbindungen</em>&gt;</code> durch die Anzahl der Verbindungen.</td>
  </tr>
  </tbody></table>
  </dd>
  </dl>

  <br />



## Annotationen für HTTPS- und TLS/SSL-Authentifizierung
{: #https-auth}


### Angepasste HTTP- und HTTPS-Ports (custom-port)
{: #custom-port}

Änderung der Standardports für den HTTP-Netzverkehr (Port 80) und den HTTPS-Netzverkehr (Port 443).
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Standardmäßig ist die Ingress-Lastausgleichsfunktion für Anwendungen so konfiguriert, dass er für eingehenden HTTP-Netzverkehr am Port mit der Nummer 80 und für eingehenden HTTPS-Netzverkehr am Port mit der Nummer 443 empfangsbereit ist. Sie können die Standardports ändern, um die Sicherheit der Domäne Ihrer Lastausgleichsfunktion für Anwendungen zu verbessern oder um ausschließlich einen HTTPS-Port zu aktivieren.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/custom-port: "protocol=&lt;protokoll1&gt; port=&lt;port1&gt;;protocol=&lt;protokoll2&gt;port=&lt;port2&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;protocol&gt;</code></td>
 <td>Geben Sie <strong>http</strong> oder <strong>https</strong> ein, um den Standardport für eingehenden HTTP- bzw. HTTPS-Netzverkehr zu ändern.</td>
 </tr>
 <tr>
 <td><code>&lt;port&gt;</code></td>
 <td>Geben Sie die Portnummer ein, die Sie für eingehenden HTTP- bzw. HTTPS-Netzverkehr verwenden wollen.  <p><strong>Hinweis:</strong> Wenn für HTTP oder HTTPS ein angepasster Port angegeben wird, dann sind die Standardports für HTTP und auch für HTTPS nicht mehr gültig. Um beispielsweise den Standardport für HTTPS in 8443 zu ändern, für HTTP jedoch weiterhin den Standardport zu verwenden, müssen Sie für beide Protokolle angepasste Ports festlegen: <code>custom-port: "protocol=http port=80; protocol=https port=8443"</code>.</p></td>
 </tr>
 </tbody></table>

 </dd>
 <dt>Syntax</dt>
 <dd><ol><li>Überprüfen Sie offene Ports für Ihre Lastausgleichsfunktion für Anwendungen. 
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
Die Ausgabe in der Befehlszeilenschnittstelle (CLI) ähnelt der folgenden:
<pre class="screen">
<code>NAME                     CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
public-ingress-ctl-svc   10.10.10.149   169.60.16.246   80:30776/TCP,443:30412/TCP   8d</code></pre></li>
<li>Öffnen Sie die Konfigurationsübersicht des Ingress-Controllers.
<pre class="pre">
<code>kubectl edit configmap ibm-cloud-provider-ingress-cm -n kube-system</code></pre></li>
<li>Fügen Sie die nicht dem Standard entsprechenden HTTP- und HTTPS-Ports zur Konfigurationsübersicht hinzu. Ersetzen Sie &lt;port&gt; durch den HTTP- oder HTTPS-Port, der geöffnet werden soll.
<pre class="codeblock">
<code>apiVersion: v1
kind: ConfigMap
data:
 public-ports: &lt;port1&gt;;&lt;port2&gt;
metadata:
 creationTimestamp: 2017-08-22T19:06:51Z
 name: ibm-cloud-provider-ingress-cm
 namespace: kube-system
 resourceVersion: "1320"
 selfLink: /api/v1/namespaces/kube-system/configmaps/ibm-cloud-provider-ingress-cm
 uid: &lt;uid&gt;</code></pre></li>
 <li>Überprüfen Sie, ob der Ingress-Controller mit den nicht dem Standard entsprechenden Ports neu konfiguriert wurde.
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
Die Ausgabe in der Befehlszeilenschnittstelle (CLI) ähnelt der folgenden:
<pre class="screen">
<code>NAME                     CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
public-ingress-ctl-svc   10.10.10.149   169.60.16.246   &lt;port1&gt;:30776/TCP,&lt;port2&gt;:30412/TCP   8d</code></pre></li>
<li>Konfigurieren Sie Ingress zur Verwendung der nicht dem Standard entsprechenden Ports bei der Weiterleitung von eingehendem Netzverkehr an Ihre Services. Verwenden Sie die YAML-Beispieldatei in dieser Referenz. </li>
<li>Aktualisieren Sie Ihre Ingress-Controllerkonfiguration.
<pre class="pre">
<code>kubectl apply -f &lt;yaml-datei&gt;</code></pre>
</li>
<li>Öffnen Sie Ihren bevorzugten Web-Browser, um auf Ihre App zuzugreifen. Beispiel: <code>https://&lt;ibm_domäne&gt;:&lt;port&gt;/&lt;servicepfad&gt;/</code></li></ol></dd></dl>

<br />



### HTTP-Weiterleitungen an HTTPS (redirect-to-https)
{: #redirect-to-https}

Konvertierung von unsicheren HTTP-Clientanforderungen in HTTPS.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Sie konfigurieren Ihre Ingress-Lastausgleichsfunktion für Anwendungen für die Sicherung Ihrer Domäne mit dem von IBM bereitgestellten TLS-Zertifikat oder Ihrem angepassten TLS-Zertifikat. Manche Benutzer versuchen unter Umständen, auf Ihre Apps zuzugreifen, indem Sie eine unsichere HTTP-Anforderung an die Domäne Ihrer Lastausgleichsfunktion für Anwendungen senden, z. B. <code>http://www.myingress.com</code>, anstatt <code>https</code> zu verwenden. Sie können die 'redirect'-Annotation verwenden, um unsichere HTTP-Anforderungen immer in HTTPS zu konvertieren. Wenn Sie diese Annotation nicht verwenden, werden unsichere HTTP-Anforderungen nicht standardmäßig in HTTPS-Anforderungen konvertiert und machen unter Umständen vertrauliche Daten ohne Verschlüsselung öffentlich zugänglich.

</br></br>
Das Umadressieren von HTTP-Anforderungen in HTTPS ist standardmäßig inaktiviert.</dd>

<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/redirect-to-https: "True"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>
</dd></dl>

<br />



### Gegenseitige Authentifizierung (mutual-auth)
{: #mutual-auth}

Konfigurieren Sie gegenseitige Authentifizierung für die Lastausgleichsfunktion für Anwendungen.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Konfigurieren Sie gegenseitige Authentifizierung für die Ingress-Lastausgleichsfunktion für Anwendungen. Der Client authentifiziert den Server und der Server authentifiziert den Client anhand von Zertifikaten. Die gegenseitige Authentifizierung wird auch als zertifikatbasierte Authentifizierung oder Zweiwegeauthentifizierung bezeichnet.
</dd>

<dt>Voraussetzungen</dt>
<dd>
<ul>
<li>[Sie müssen über einen geheimen Schlüssel verfügen, der die erforderliche Zertifizierungsstelle (CA) enthält](cs_app.html#secrets). Außerdem werden die Dateien <code>client.key</code> und <code>client.crt</code> für die gegenseitige Authentifizierung benötigt.</li>
<li>Um die gegenseitige Authentifizierung an einem anderen Port als 443 zu ermöglichen, [konfigurieren Sie die Lastausgleichsfunktion zum Öffnen des gültigen Ports](cs_ingress.html#opening_ingress_ports).</li>
</ul>
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/mutual-auth: "secretName=&lt;mein_geheimer_schlüssel&gt; port=&lt;port&gt; serviceName=&lt;servicename1&gt;,&lt;servicename2&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080
          </code></pre>

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
</thead>
<tbody>
<tr>
<td><code>secretName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_geheimer_schlüssel</em>&gt;</code> durch einen Namen für die Ressource mit dem geheimen Schlüssel.</td>
</tr>
<tr>
<td><code>&lt;port&gt;</code></td>
<td>Die Nummer des Ports der Lastausgleichsfunktion für Anwendungen.</td>
</tr>
<tr>
<td><code>&lt;serviceName&gt;</code></td>
<td>Der Namen von mindestens einer Ingress-Ressource. Dieser Parameter ist optional.</td>
</tr>
</tbody></table>

</dd>
</dl>

<br />



### Unterstützung für SSL-Services (ssl-services)
{: #ssl-services}

Lassen Sie HTTPS-Anforderungen zu und verschlüsseln Sie Datenverkehr zu Ihren Upstream-Apps.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Verschlüsseln Sie den Datenverkehr zu Ihren Upstream-Apps, für die HTTPS erforderlich ist, mit den Lastausgleichsfunktionen für Anwendungen.

**Optional**: Sie können die [unidirektionale Authentifizierung oder die gegenseitige Authentifizierung](#ssl-services-auth) zu dieser Annotation hinzufügen.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: &lt;mein_ingress-name&gt;
  annotations:
    ingress.bluemix.net/ssl-services: "ssl-service=&lt;mein_service1&gt; [ssl-secret=&lt;geheimer_ssl-schlüssel_für_service1&gt;];ssl-service=&lt;mein_service2&gt; [ssl-secret=&lt;geheimer_ssl-schlüssel_für_service2&gt;]
spec:
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service1
          servicePort: 8443
      - path: /
        backend:
          serviceName: mein_service2
          servicePort: 8444</code></pre>

<table>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
  </thead>
  <tbody>
  <tr>
  <td><code>ssl-service</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Service, der Ihre App darstellt. Der Datenverkehr wird von der Lastausgleichsfunktion für Anwendungen zu dieser App verschlüsselt.</td>
  </tr>
  <tr>
  <td><code>ssl-secret</code></td>
  <td>Ersetzen Sie <code>&lt;<em>geheimer_ssl-schlüssel_für_service</em>&gt;</code> durch den geheimen Schlüssel für den Service. Dieser Parameter ist optional. Wenn der Parameter bereitgestellt wird, muss der Wert den Schlüssel und das Zertifikat enthalten, den/das die App vom Client erwartet.</td>
  </tr>
  </tbody></table>

  </dd>
</dl>

<br />


#### Unterstützung für SSL-Services mit Authentifizierung
{: #ssl-services-auth}

Lassen Sie HTTPS-Anforderungen zu und verschlüsseln Sie Datenverkehr zu Ihren Upstream-Apps für zusätzliche Sicherheit mit der unidirektionalen oder gegenseitigen Authentifizierung.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Konfigurieren Sie die gegenseitige Authentifizierung für Lastausgleichs-Apps, für die HTTPS erforderlich ist, mit den Ingress-Controllern.

**Hinweis**: Bevor Sie beginnen, [konvertieren Sie das Zertifikat und den Schlüssel in die Base64-Codierung ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.base64encode.org/).

</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: &lt;mein_ingress-name&gt;
  annotations:
    ingress.bluemix.net/ssl-services: |
      ssl-service=&lt;mein_service1&gt; ssl-secret=&lt;geheimer_ssl-schlüssel_für_service1&gt;;
      ssl-service=&lt;mein_service2&gt; ssl-secret=&lt;geheimer_ssl-schlüssel_für_service2&gt;
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service1
          servicePort: 8443
      - path: /
        backend:
          serviceName: mein_service2
          servicePort: 8444
          </code></pre>

<table>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
  </thead>
  <tbody>
  <tr>
  <td><code>ssl-service</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Service, der Ihre App darstellt. Der Datenverkehr wird von der Lastausgleichsfunktion für Anwendungen zu dieser App verschlüsselt.</td>
  </tr>
  <tr>
  <td><code>ssl-secret</code></td>
  <td>Ersetzen Sie <code>&lt;<em>geheimer_ssl-schlüssel_für_service</em>&gt;</code> durch den geheimen Schlüssel für den Service. Dieser Parameter ist optional. Wenn der Parameter bereitgestellt wird, muss der Wert den Schlüssel und das Zertifikat enthalten, den/das die App vom Client erwartet.</td>
  </tr>
  </tbody></table>

  </dd>
  </dl>


<br />



