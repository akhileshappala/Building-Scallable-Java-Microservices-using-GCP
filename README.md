# Java-Microservices-using-GCP
Step wise guide in GCP


Cloud PUB/SUB
1.Depedency to be added to application pom
<dependency>
            <groupId>org.springframework.integration</groupId>
            <artifactId>spring-integration-core</artifactId>
       </dependency>
       
 2. OutboundGateway.java for the application to send a text msg
package com.example.frontend;
import org.springframework.integration.annotation.MessagingGateway;
@MessagingGateway(defaultRequestChannel = "messagesOutputChannel")
public interface OutboundGateway {
        void publishMessage(String message);
}
3. Whenever someone posts a new guestbook message, OutboundGateway also sends it to a messaging system. At this point, the application does not know what messaging system is being used.
    @Autowired
    private OutboundGateway outboundGateway;
4. 

    pubSubTemplate.publish("messages", name + ": " + message);

5. @Bean
    @ServiceActivator(inputChannel = "messagesOutputChannel")
    public MessageHandler messageSender(PubSubTemplate pubsubTemplate) {
        return new PubSubMessageHandler(pubsubTemplate, "messages");
    }
