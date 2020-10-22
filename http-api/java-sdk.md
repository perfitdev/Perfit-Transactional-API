---
description: Contamos con una librería para facilitar el uso de la API desde Java.
---

# Java SDK

## Instalación

Las formas más comunes de incluir la SDK en los proyectos es utilizando Maven o Gradle. 

### Maven

```markup
<dependency>
    <groupId>com.myperfit.sdk.transactional</groupId>
    <artifactId>transactionalsdk</artifactId>
    <version>[1.0,2.0)</version>
</dependency>
```

### Gradle

```javascript
compile group: 'com.myperfit.sdk.transactional', name: 'transactionalsdk', version: '1.+'
```

## Uso básico

```java
PerfitTransactional perfit = PerfitTransactional.builder()
        .apiKey("API_KEY")
        .build();

// Remitente
MailAddressRequest fromAddress = MailAddressRequest.builder()
        .email("from@midominio.com")
        .name("Nombre Remitente")
        .build();

// Contenidos
MailContentRequest content = MailContentRequest.builder()
        .html("contenido html")
        .build();

// Listado de destinatarios
List<MailRecipientRequest> recipients = new ArrayList<>();

MailAddressRequest toAddress1 = MailAddressRequest.builder()
        .email("to@midominio.com")
        .name("Nombre Destinatario") 
        .build();
        
MailRecipientRequest recipient1 = MailRecipientRequest.builder()
        .to(toAddress1)
        .customArgs(Map.of("key1","value1", "key2", "value2"))
        .build();
        
recipients.add(recipient1);

// Mensaje completo
SendMailRequest request = SendMailRequest.builder()
        .from(fromAddress)
        .subject("Test Subject")
        .content(content)
        .recipients(recipients)
        .tags(List.of("tag1", "tag2"))
        .build();

try {
        // Envío del email
        perfit.send(request);
} catch (RequestFailedException ex) {
        // Manejar excepciones
}
```



