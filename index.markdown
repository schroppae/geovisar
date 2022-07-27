---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
---
<script src="assets/qrcodejs/jquery.min.js"></script>
<script src="assets/qrcodejs/qrcode.min.js"></script>

# GeoVisAR

Mit Hilfe von GeoVisAR könen auf einfache Weise Geodaten über webbasiertes Augmented Reality mit dem Smartphone erlebbar gemacht werden. In dieser Beispiel Anwendung werden Marker rund um das Hochschulzentrum der FOM in München mit Informationen für neue Studierende angezeigt. Über ein einfaches Forken des GitHub Repositorys wird es aber auch Interessierten ohne Programmierkenntnisse möglich webbasierte Augmented Reality Anwendungen zu erstellen und kostenlos über GitHub Pages zu veröffentlichen. Eine Anleitung für die notwendigen Anpassungen findet sich in der README des Repositorys.



<form action="{{ site.baseurl }}/app/index.html" method="get" target="_blank" style="text-align: center"><button style="
background-color: #4CAF50;
border: none;
color: white;
padding: 15px 32px;
text-align: center;
text-decoration: none;
display: inline-block;
font-size: 16px;
margin: 4px 2px;
cursor: pointer;">AR-Anwendung starten</button></form>

<div style="text-align: center">Nutzung mit Smartphone empfohlen!</div>
<div style="text-align: center">(Es werden Standort- und Kameraberechtigungen abgefragt)</div>


<br>
<p style="text-align: center"><b>Um diese Seite auf dem Smartphone zu öffnen einfach diesen QR-Code scannen:</b></p>
<div style="display: flex; justify-content: center; text-align: center;" id="qrcode"></div>
<script type="text/javascript">
new QRCode(document.getElementById("qrcode"), "{{ site.url }}{{ site.baseurl }}");
</script>
<br>

### Beispielbilder: 
![Intro](assets/intro-image.jpg)

[Tipps](hints.html)