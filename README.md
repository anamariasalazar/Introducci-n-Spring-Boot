# Introducci-n-Spring-Boot

#  Starting with Spring Initializr

>[Spring initializr](https://start.spring.io/) 
> 
#  Create a Simple Web Application

> Now you can create a web controller for a simple web application, as the following listing ```src/main/java/com/example/springboot/HelloController.java``` shows:
> 
```java
package com.example.springboot;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

	@GetMapping("/")
	public String index() {
		return "Greetings from Spring Boot!";
	}
  }
```
>
#  Create an Application class

> You need to modify the application class to match the following listing from ```src/main/java/com/example/springboot/Application.java``` 
> 
```java
package com.example.springboot;

import java.util.Arrays;

import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

	@Bean
	public CommandLineRunner commandLineRunner(ApplicationContext ctx) {
		return args -> {

			System.out.println("Let's inspect the beans provided by Spring Boot:");

			String[] beanNames = ctx.getBeanDefinitionNames();
			Arrays.sort(beanNames);
			for (String beanName : beanNames) {
				System.out.println(beanName);
			}
		};
	}
}
```
>
#  Run the Application

> Run the following command in a terminal window ```mvnw spring-boot:run``` 
> 
> You should see output similar to the following:
```
Let's inspect the beans provided by Spring Boot:
application
beanNameHandlerMapping
defaultServletHandlerMapping
dispatcherServlet
embeddedServletContainerCustomizerBeanPostProcessor
handlerExceptionResolver
helloController
httpRequestHandlerAdapter
messageSource
mvcContentNegotiationManager
mvcConversionService
mvcValidator
org.springframework.boot.autoconfigure.MessageSourceAutoConfiguration
org.springframework.boot.autoconfigure.PropertyPlaceholderAutoConfiguration
org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration
org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration$DispatcherServletConfiguration
org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration$EmbeddedTomcat
org.springframework.boot.autoconfigure.web.ServerPropertiesAutoConfiguration
org.springframework.boot.context.embedded.properties.ServerProperties
org.springframework.context.annotation.ConfigurationClassPostProcessor.enhancedConfigurationProcessor
org.springframework.context.annotation.ConfigurationClassPostProcessor.importAwareProcessor
org.springframework.context.annotation.internalAutowiredAnnotationProcessor
org.springframework.context.annotation.internalCommonAnnotationProcessor
org.springframework.context.annotation.internalConfigurationAnnotationProcessor
org.springframework.context.annotation.internalRequiredAnnotationProcessor
org.springframework.web.servlet.config.annotation.DelegatingWebMvcConfiguration
propertySourcesBinder
propertySourcesPlaceholderConfigurer
requestMappingHandlerAdapter
requestMappingHandlerMapping
resourceHandlerMapping
simpleControllerHandlerAdapter
tomcatEmbeddedServletContainerFactory
viewControllerHandlerMapping
```
> Now run the service with curl (in a separate terminal window), by running the following command (shown with its output): ```curl localhost:8080``` para consultar 
> 
> ![](/imagenes/1.PNG)
> 
#  Add Unit Tests

> Add the following to your pom.xml file
>
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-test</artifactId>
	<scope>test</scope>
</dependency>
```
> Vamos a crear el archivo java ```src/test/java/com/example/springboot/HelloControllerTest.java``` y en el vamos a escribir lo siguiente
> ```java
> paquete com.ejemplo.springboot;
>
> importar org.hamcrest.Matchers.equalTo estático;
> importar org.springframework.test.web.servlet.result.MockMvcResultMatchers.content estático;
> importar org.springframework.test.web.servlet.result.MockMvcResultMatchers.status estático;
> importar org.junit.jupiter.api.Test;
> importar org.springframework.beans.factory.annotation.Autowired;
> importar org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
> importar org.springframework.boot.test.context.SpringBootTest;
> importar org.springframework.http.MediaType;
> importar org.springframework.test.web.servlet.MockMvc;
> importar org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
> 
> @SpringBootTest
> @AutoConfigureMockMvc
> clase pública HelloControllerTest {
> 
>  	@autocableado
>  	privado MockMvc mvc;
> 
>  	@Prueba
>  	public void getHello() lanza Excepción {
>  		mvc.perform(MockMvcRequestBuilders.get("/").accept(MediaType.APPLICATION_JSON))
>  				.andExpect(status().isOk())
>  				.andExpect(content().string(equalTo("¡Saludos desde Spring Boot!")));
>  	}
> }
> ```
> Ahora crearemos el archivo java ```src/test/java/com/example/springboot/HelloControllerIT.java``` y en el vamos a escribir lo siguiente
> ```java
> paquete com.ejemplo.springboot;
>
> importar org.junit.jupiter.api.Test;
> importar org.springframework.beans.factory.annotation.Autowired;
> importar org.springframework.boot.test.context.SpringBootTest;
> importar org.springframework.boot.test.web.client.TestRestTemplate;
> importar org.springframework.http.ResponseEntity;
> importar org.assertj.core.api.Assertions.assertThat estático;
>
> @SpringBootTest(entorno web = SpringBootTest.WebEnvironment.RANDOM_PORT)
> clase pública HelloControllerIT {
>
>  	@autocableado
>  	plantilla TestRestTemplate privada;
> 
>      @Prueba
>      public void getHello() lanza Excepción {
>          ResponseEntity<String> respuesta = template.getForEntity("/", String.class);
>          assertThat(response.getBody()).isEqualTo("¡Saludos desde Spring Boot!");
>      }
> }
> ```
#  Agregar servicios de producción

> Agregamos la siguiente dependencia al pom para poder usar los servicios de actuador
>
> ```
> <dependencia>
>  	<groupId>org.springframework.boot</groupId>
>  	<artifactId>actuador-arranque-de-resorte</artifactId>
> </dependencia>
> ```
> Ahora ejecutamos ```mvnw spring-boot:run``` para correr la aplicación
>
> ```
> management.endpoint.configprops-org.springframework.boot.actuate.autoconfigure.context.properties.ConfigurationPropertiesReportEndpointProperties
> administración.endpoint.env-org.springframework.boot.actuate.autoconfigure.env.EnvironmentEndpointProperties
> administración.endpoint.health-org.springframework.boot.actuate.autoconfigure.health.HealthEndpointProperties
> administración.endpoint.logfile-org.springframework.boot.actuate.autoconfigure.logging.LogFileWebEndpointProperties
> administración.endpoints.jmx-org.springframework.boot.actuate.autoconfigure.endpoint.jmx.JmxEndpointProperties
> administración.endpoints.web-org.springframework.boot.actuate.autoconfigure.endpoint.web.WebEndpointProperties
> administración.puntos finales.web.cors-org.springframework.boot.actuate.autoconfigure.endpoint.web.CorsEndpointProperties
> management.health.diskspace-org.springframework.boot.actuate.autoconfigure.system.DiskSpaceHealthIndicatorProperties
> gestión.info-org.springframework.boot.actuate.autoconfigure.info.InfoContributorProperties
> administración.metrics-org.springframework.boot.actuate.autoconfigure.metrics.MetricsProperties
> administración.metrics.export.simple-org.springframework.boot.actuate.autoconfigure.metrics.export.simple.SimpleProperties
> administración.servidor-org.springframework.boot.actuate.autoconfigure.web.server.ManagementServerProperties
> ```
>
> Ahora ejecutamos el comando ```curl localhost:8080/actuator/health``` en nuestra terminal para saber el estado de ese puerto y obtenemos
>
> ![](/img/resultado2.PNG)
>
> Finalmente ejecutamos el comando ```curl -X POST localhost:8080/actuator/shutdown``` en nuestra terminal para terminar la conexión y obtenemos
>
> ![](/img/resultado3.PNG)


Licencia bajo la [ GNU General Public License ](/LICENSE).
