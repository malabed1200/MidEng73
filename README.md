# DEZSYS_GK73_WAREHOUSE_MOM – Protokoll (GK)

## 1. Einführung
In dieser Übung wurde eine Message Oriented Middleware (MOM) zur Kommunikation zwischen einem Lagerstandort und einer Zentrale implementiert.  
Als Message Broker wurde Apache Kafka eingesetzt. Die Kommunikation erfolgt asynchron und nachrichtenbasiert.

Ein Lagerstandort sendet seine Daten über eine REST-Schnittstelle an Kafka.  
Die Zentrale empfängt diese Daten über einen Kafka Consumer.

---

## 2. Architekturübersicht

**Komponenten:**
- Apache Kafka (KRaft-Standalone-Modus)
- Spring Boot Applikation
  - REST Controller (Producer)
  - Kafka Producer
  - Kafka Consumer
- Kafka Topic: `quickstart-events`

**Ablauf:**
1. HTTP-Request an `/send`
2. Nachricht wird an Kafka gesendet
3. Consumer liest Nachricht aus dem Topic
4. Ausgabe der Nachricht auf der Konsole

---

## 3. Technische Voraussetzungen
- Windows 10/11
- Java JDK
- Apache Kafka 4.1.1
- IntelliJ IDEA
- Gradle
- Spring Boot

---

## 4. Installation und Konfiguration

### 4.1 Apache Kafka
Kafka wurde lokal installiert unter:
C:\kafka_2.13-4.1.1


Der Broker wurde im **KRaft-Standalone-Modus** betrieben (ohne Zookeeper).

Initialisierung des Storage:
bin\windows\kafka-storage.bat format --standalone -t <UUID> -c config\server.properties


Start des Brokers:
bin\windows\kafka-server-start.bat config\server.properties


---

### 4.2 Topic-Erstellung
Das Kafka-Topic wurde mit folgendem Befehl erstellt:
bin\windows\kafka-topics.bat --create --topic quickstart-events --bootstrap-server localhost:9092


---

## 5. Implementierung

### 5.1 REST Producer
Nachrichten werden über folgenden REST-Endpunkt an Kafka gesendet:
http://localhost:8080/send?message=HalloKafka


---

### 5.2 Kafka Consumer
Der Consumer lauscht auf das Topic `quickstart-events` und gibt empfangene Nachrichten in der Konsole aus:
Read from Message Queue: HalloKafka


---

## 6. Testdurchführung

**Testfall:**
- Aufruf des REST-Endpunkts im Browser
- Versand der Nachricht „HalloKafka“

**Ergebnis:**
- Nachricht wurde erfolgreich an Kafka gesendet
- Nachricht wurde erfolgreich vom Consumer empfangen

---

## 7. Erfüllung der GK-Anforderungen

| Anforderung | Status |
|------------|--------|
| Kafka installiert | ✔ |
| Kommunikation Lager → Zentrale | ✔ |
| Message Queue / Topic | ✔ |
| Ausgabe der empfangenen Daten | ✔ |
| Message Oriented Middleware | ✔ |

---

## 8. Fazit
Die Übung demonstriert erfolgreich die Verwendung einer Message Oriented Middleware mit Apache Kafka.  
Durch die lose Kopplung zwischen Producer und Consumer ist das System flexibel und erweiterbar.

---

