# Introducci-n-Spring-Boot

#  Creación proyecto con primavera

> Podemos hacer uso de la herrramienta que nos brinda la pagina web de spring boot [Spring initializr](https://start.spring.io/) para crear la aplicación
#  Creación aplicación web

> Vamos a crear el archivo java ```src/main/java/com/example/springboot/HelloController.java``` y en el vamos a escribir lo siguiente
> ```java
> paquete com.ejemplo.springboot;
>
> importar org.springframework.web.bind.annotation.GetMapping;
> importar org.springframework.web.bind.annotation.RestController;
>
> @RestController
> clase pública HelloController {
>
> 	@ObtenerMapeo("/")
>  	índice público de cadenas () {
>  		return "¡Saludos desde Spring Boot!";
>  	}
>
> }
> ```
#  Crear aplicacion de clase

> Vamos a crear el archivo java ```src/main/java/com/example/springboot/Application.java``` y en el vamos a escribir lo siguiente
> ```java
> paquete com.ejemplo.springboot;
>
> importar java.util.Arrays;
> importar org.springframework.boot.CommandLineRunner;
> importar org.springframework.boot.SpringApplication;
> importar org.springframework.boot.autoconfigure.SpringBootApplication;
> importar org.springframework.context.ApplicationContext;
> importar org.springframework.context.annotation.Bean;
>
> @SpringBootApplication
> Aplicación de clase pública {
>
>  	public static void main(String[] args) {
>  		SpringApplication.run(Application.class, args);
>  	}
>
>  	@frijol
>  	público CommandLineRunner commandLineRunner (Contexto de aplicación ctx) {
>  		devolver argumentos -> {
>
>  			System.out.println("Veamos los beans proporcionados por Spring Boot:");
> 
>  			String[] beanNames = ctx.getBeanDefinitionNames();
>  			Arrays.sort(beanNames);
>  			for (String beanName : beanNames) {
>  				System.out.println(beanName);
>  			}
>
>  		};
>  	}
>
> }
> ```
#  Ejecutar aplicación

> Corremos el siguiente comando ```mvnw spring-boot:run``` en nuestra terminal y obtenemos lo siguiente
>
> ```
> Inspeccionemos los beans proporcionados por Spring Boot:
> solicitud
> beanNameHandlerMapping
> asignación predeterminada de ServletHandler
> despachadorServlet
> EmbeddedServletContainerCustomizerBeanPostProcessor
> handlerExceptionResolver
> holaControlador
> httpRequestHandlerAdapter
> fuente del mensaje
> mvcContentNegotiationManager
> mvcConversionService
> mvcValidador
> org.springframework.boot.autoconfigure.MessageSourceAutoConfiguration
> org.springframework.boot.autoconfigure.PropertyPlaceholderAutoConfiguration
> org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration
> org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration$DispatcherServletConfiguration
> org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration$EmbeddedTomcat
> org.springframework.boot.autoconfigure.web.ServerPropertiesAutoConfiguration
> org.springframework.boot.context.embedded.properties.ServerProperties
> org.springframework.context.annotation.ConfigurationClassPostProcessor.enhancedConfigurationProcessor
> org.springframework.context.annotation.ConfigurationClassPostProcessor.importAwareProcessor
> org.springframework.context.annotation.internalAutowiredAnnotationProcessor
> org.springframework.context.annotation.internalCommonAnnotationProcessor
> org.springframework.context.annotation.internalConfigurationAnnotationProcessor
> org.springframework.context.annotation.internalRequiredAnnotationProcessor
> org.springframework.web.servlet.config.annotation.DelegatingWebMvcConfiguration
> propertySourcesBinder
> propertySourcesPlaceholderConfigurer
> solicitudMappingHandlerAdapter
> requestMappingHandlerMapping
> sourceHandlerMapping
> mpleControllerHandlerAdapter
> mcatEmbeddedServletContainerFactory
> wControllerHandlerMapping
> ```
> Ahora ejecutamos el siguiente comando ```curl localhost:8080``` para consultar hacia lo que se encuentra en localhost en el puerto 8080 en este momento, obtenemos como resultado
> 
> ![](/img/resultado1.PNG)
#  Pruebas de unidad

> Agregamos la siguiente dependencia a nuestro pom para poder ejecutar las pruebas
>
> ```xml
> <dependencia>
>  	<groupId>org.springframework.boot</groupId>
>  	<artifactId>prueba de inicio de arranque de resorte</artifactId>
>  	<alcance>prueba</alcance>
> </dependencia>
> ```
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
