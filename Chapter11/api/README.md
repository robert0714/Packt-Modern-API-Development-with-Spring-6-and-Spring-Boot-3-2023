# Configuring the gRPC API library project
You have configured the artifact used by the Protobuf compiler (protoc) and its Java plugin (protoc-gen-grpc-java), which will generate the Java code based on .proto files.
When you run the ``gradle build`` command for the first time, Gradle will download the protoc and protoc-gen-grpc-java executables based on the OS.

# Publishing the payment gateway service gRPC server, stubs, and models
You can use the following command, which should be executed from the api project’s root directory:

```bash
# Make sure to enable UTF-8 for file encoding because# we are using UTF characters in Java files.
$ export JAVA_TOOL_OPTIONS="-Dfile.encoding=UTF8"
$ gradle clean publishToMavenLocal
```


With the preceding command, you are setting the file encoding to UTF-8 first because we are using the UTF characters in Java files. Then, you are performing clean, build, and publish operations. The second command will first remove the existing files. Then, it will generate the Java files (the **generateProto** Gradle task) from the Protobuf file, build it (the build Gradle task), and publish the artifact to your local Maven repository (the **publishToMavenLocal** Gradle task).

The **generateProto** Gradle task will generate the two types of Java classes in two directories, as shown next:

* **Models**: This Protobuf Gradle plugin generates messages (aka models) and classes in separate Java files in the ``/api/lib/build/generated/source/proto/main/java`` directory, such as **Card.java** or **Address.java**. This directory will also contain the Java files of request and response objects used in operation contracts, such as CreateChargeReq, CreateSourceReq, **Charge.java**, and **Source.java**.
* **gRPC classes**: This Protobuf Gradle plugin generates the service definitions of both services (**ChargeServiceGrpc.java** and **SourceServiceGrpc .java**) in the ``/api/lib/build/generated/source/proto/main/grpc`` directory. Each of these gRPC Java files contains a base class, stub classes, and methods for each operation defined in the service descriptor for the **Charge** and **Source** services.