# 8. Lerneinheit

## Metadaten modellieren und Schnittstellen nutzen

Liebes Tagebuch

Bei dieser Unterrichtseinheit gab es viele Inputs und Themen, welche behandelt wurden. Ausserdem ist es ein Thema, was sehr komplex ist und ich nicht viel Erfahrung dazu habe. Dies macht es zusätzlich schwierig darüber zu berichten. Ich werde zwei Themen, welche ich vertiefter anschauen möchte, genauer behandeln: Zum einen die unterschiedlichen Austauschprotokolle für Metadaten und zum anderen XLST mit Beispielen.

### Austauschprotokolle für Metadaten
Ich fand es sehr spannend zu hören, dass es Austauschprotokolle für Metadaten gibt und auch, dass es unterschiedliche gibt. Ich weiss was Metadaten sind, jedoch habe ich mir nie Gedanken gemacht, wie diese ausgetauscht werden können. Es gibt drei bekannte: [Z39.50](https://www.loc.gov/z3950/agency/), [SRU](https://www.loc.gov/standards/sru/) und [OAI-PMH](https://www.openarchives.org/pmh/).

Bei Z39.50 sieht man nur schon an der Webseite, dass es ziemlich halt ist (letztes Update im November 2015 – das Design war da vermutlich schon 10-Jährig). Gemäss der Webseite ist Z39.50 
> “a client/server based protocol for searching and retrieving information from remote databases”. 

SRU ist ein Protokoll für Suchanfragen, welches auf XML basiert. Es ist die Weiterentwicklung vom Z39.50 Protokoll und wird mit der Retrievalsprache CQL formuliert. Beispielsweise hat die [Deutsche Nationalbibliothek](https://www.dnb.de/DE/Professionell/Metadatendienste/Datenbezug/SRU/sru.html) eine SRU-Schnittstelle eingebaut. Mit SRU kann man mit Suchindizes und -begriffe Daten der DNB suchen und in die eigene Umgebung übernehmen. Ich stell mir das sehr praktisch vor, wenn solche universellen Daten miteinander (wie mir scheint ziemlich einfach) ausgetauscht werden können. Ein Beispiel von einer CQL-Abfrage ist sieht man unten. Es sieht sehr ähnlich wie SQL aus. 

```
SELECT * | select_expression | DISTINCT partition 
FROM [keyspace_name.] table_name 
[WHERE partition_value
   [AND clustering_filters 
   [AND static_filters]]] 
[ORDER BY PK_column_name ASC|DESC] 
[LIMIT N]
[ALLOW FILTERING]
```

*OAI-PMH* ist das Austauschprotokoll, welches wir im Unterricht anschauen. 
Datenanbeiter sind Repositories, welche Metadaten über OAI-PMH Schnittstellen bereitstellen. Die Provider stellen die Anfragen an diese Anbieter, um die Daten zu sammeln, welche über http aufgerufen werden. Eine Implementation von OAI-PMH muss Metadaten enthalten, welche dem Dublin Core Standard entsprechen. Ggf. können sie auch zusätzliche Darstellungen unterstützen. Ein Beispiel einer OAI-Abfrage ist unten aufgeführt.
```
https://services.dnb.de/oai/repository?verb=GetRecord&metadataPrefix=MARC21-xml&identifier=oai:dnb.de/authorities/118540238
```

### XSL Transformation
Wir haben XLST als Crosswalks (Konvertierung von einem Metadatenstandard in einen anderen) angeschaut. XLST ist eine Programmiersprache zur Transformation von XML Dokumenten. Es baut auf der logischen Baumstruktur des XML auf und dient der Definition von Umwandlungsregeln. 

Wir haben die Transformation von Dublin Core zu Marc21 mittels dem Tool [XSL Transform](http://xsltransform.net) angeschaut und ich fand es sehr spannend zu sehen, wie die (einfache) Datei von DC zu Marc21 mittels dem Tool klappte. Komplexere Dateien (z.B. solche welche Verweise auf andere Dateien haben) kann das Tool nicht umwandeln. Dazu dient die Software MarcEdit. 

Als ich u XLST recherchiert habe, sind mir einige spannende Codeschnippsel aufgefallen. Ich wusste gar nicht dass man mit XSL beispielsweise if…else… abbilden kann ;-)
```
<xsl:choose>
  <xsl:when test="...">...</xsl:when>
  <xsl:when test="...">...</xsl:when>
  <xsl:when test="...">...</xsl:when>
  <xsl:otherwise>...</xsl:otherwise>
</xsl:choose>
```
Oder eine for-each Schleife (inkl. Sortierung!)
```
<xsl:for-each select="buch">
  <xsl:sort select="preis" order="ascending" />
</xsl:for-each>
```
Und zu guter letzt noch das choose Element, welches mehrere Bedingungen abbilden zu können.
```
<xsl:choose>
  <xsl:when test="expression">
    ... some output ...
  </xsl:when>
  <xsl:otherwise>
    ... some output ....
  </xsl:otherwise>
</xsl:choose>
```
… sehr spannend was man damit alles machen kann. 



[Zurück zur Übersicht ›](../README.md)
