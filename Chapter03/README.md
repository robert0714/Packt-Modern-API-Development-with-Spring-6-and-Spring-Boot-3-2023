# Chpater 3 API Specifications and Implementation
We have chosen a design-first approach for implementation to make our development process understandable for non-technical stakeholders as well. To make this approach possible, we will make use of the **OpenAPI Specification** (OAS) to, first, design an API and, later, implement it. 

We’ll cover the following topics as part of this chapter:

* Designing APIs with OAS
* Understanding the basic structure of OAS
* Converting OAS to Spring code
* Implementing the OAS code interfaces
* Adding a Global Exception Handler
* Testing the implementation of the controllers

##  Designing APIs with OAS
You should use the **design-first approach**.

We’ll use version 3.0 of OAS (https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.3.md) to implement the e-commerce app REST API. We’ll use YAML (pronounced as yamel, rhyming with camel), which is cleaner and easier to read. YAML is also space-sensitive. It uses space for indentation; for example, it represents the key: value pair (pay attention to the space after the colon – :). You can read more about YAML at https://yaml.org/spec/.

We’ll make use of the following Swagger tools in this chapter:

* **Swagger Editor**(https://editor.swagger.io/): This tool is used to design and describe the e-commerce app REST APIs. It allows you to write and preview, at the same time, your REST APIs’ design and description. Make sure that you use OAS 3.0. Its beta version is available at https://editor-next.swagger.io/.
* **Swagger Codegen**(https://github.com/swagger-api/swagger-codegen): This tool is used to generate the Spring-based API models and Java interfaces. You’ll use the Gradle plugin (https://github.com/int128/gradle-swagger-generator-plugin) to generate code that works on top of Swagger Codegen. There is also an OpenAPI tool Gradle plugin – OpenAPI Generator (https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator-gradle-plugin). However, we’ll opt for the former one because of the open issues count, which is 3.2k (there are multiple for Java/Spring as well) at the time of writing.
* **Swagger UI**(https://swagger.io/swagger-ui/): This tool is used to generate the REST API documentation. The same Gradle plugin will be used to generate the API documentation.


# Summary
In this chapter, we opted for the design-first approach to writing RESTful web services. You learned how to write an API description using OAS and how to generate models and API Java interfaces using the Swagger Codegen tool (using the Gradle plugin). We also implemented a Global Exception Handler to centralize the handling of all the exceptions. Once you have the API Java interfaces, you can write their implementations for business logic. Now, you know how to use OAS and Swagger Codegen to write RESTful APIs. You also now know how to handle exceptions globally.

In the next chapter, we’ll implement fully fledged API Java interfaces with business logic with database persistence.

# Questions
1. What is OpenAPI and how does it help?  
1. How can you define a nested array in a model in a YAML OAS-based file?  
1. What annotations do we need to implement a Global Exception Handler?  
1. How can you use models or classes written in Java code in your OpenAPI description?  
1. Why do we only generate models and API Java interfaces using Swagger Codegen?  
# Answers
1. OAS was introduced to solve at least a few aspects of a REST API’s specification and description. It allows you to write REST APIs in the YAML or JSON markup languages, which allows you to interact with all stakeholders, including those who are non-technical, for review and discussion in the development phase. It also allows you to generate documentation, models, interfaces, clients, and servers in different languages.
1. The array is defined using the following code:
   ```
    type: arrayitems:  type: array  items:    type: string
   ```
1. You need a class annotation, @ControllerAdvice, and a method annotation, @ExceptionHandler, to implement the Global Exception Handler.
1. You can use --type-mappings and --import-mappings rawOptions in the swaggerSources task of the build.gradle file.
1. We only generate the models and API Java interfaces using Swagger Codegen because this allows the complete implementation of controllers by developers only.
# Further reading
* OAS 3.0: https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.3.md
* The Gradle plugin for OpenAPI Codegen: https://github.com/int128/gradle-swagger-generator-plugin
* OAS Code Generator configuration options for Spring: https://openapi-generator.tech/docs/generators/spring/
* YAML specifications: https://yaml.org/spec/
* Semantic versioning: https://semver.org/