![[Pasted image 20260302202741.png]]

Searching this error page tells us that this is a 'spring boot' java web framework

Springboot has exposed directory endpoints.

By using a special springboot [[Synced OSCP Notes/Cracking/Wordlists|Wordlists]], we can discover /actuator

---

In a Spring Boot application, application-related properties are stored in a file named **`application.properties`** ==by default==. Alternatively, you can use a YAML formatted file named **`application.yml`** (or `application.yaml`). 

These files are typically located in the `src/main/resources/` directory of your project.