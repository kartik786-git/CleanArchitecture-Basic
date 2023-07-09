# CleanArchitecture-Basic

Clean Architecture | Setup Project Structure | Part 1

my Channel 
https://www.youtube.com/@poddarkktrickstech7988

Clean Architecture repo
https://github.com/kartik786-git/CleanArchitecture-Basic

Create minimal api .net 7 | Get | Post | Delete | Put | CURD Operation
https://youtu.be/iQ_IiO0-BqE

Create web api .net 7 (Controller-based) | Create | Update | Read | Delete | Operation
https://youtu.be/2eIOqoFpnWw


Clean Architecture is a software design pattern that aims to create a modular and maintainable codebase by separating concerns and dependencies. It promotes the separation of concerns through multiple layers and enforces boundaries between them. In this response, I'll provide an overview of Clean Architecture principles and show you a sample code structure in .NET 7.

Clean Architecture Principles:

Separation of Concerns: The codebase is divided into distinct layers, each with its own responsibilities and concerns.
Dependency Rule: Dependencies flow inward, meaning outer layers do not depend on inner layers. This allows for easy replacement or modification of components.

Abstraction over Implementation: Interfaces and abstractions are used to define contracts, decoupling high-level modules from low-level details.
Testability: The architecture facilitates unit testing by enabling isolated testing of components at different levels.
Independence of Frameworks: The core business logic is not dependent on any specific framework or library, making it more portable and maintainable.

Sample Code Structure:

Here's an example of a sample code structure in .NET 7 based on Clean Architecture principles:

Presentation Layer (Web/API)

This layer interacts with the user and handles HTTP requests and responses.
It depends on the Application layer.
It contains controllers, view models, and other UI-related components.

Application Layer

This layer contains application-specific business logic and coordinates interactions between the Presentation and Domain layers.
It depends on the Domain layer.
It contains use cases, application services, and mappers.

Domain Layer

This layer represents the core business logic of the application.
It is independent of other layers and contains domain models, entities, interfaces, and domain services.

Infrastructure Layer

This layer provides implementations for external dependencies, such as databases, external services, or third-party libraries.
It depends on the Domain and Application layers.
It contains data access implementations, repositories, external service clients, and other infrastructure-specific components.

## No need docker file steps

# Containerize a .NET app with dotnet publish

  <PropertyGroup>
........
	  <!--<ContainerBaseImage>mcr.microsoft.com/dotnet/runtime:6.0</ContainerBaseImage>-->
	  <ContainerImageName>webapi-image</ContainerImageName>
	  <ContainerImageTag>3.3.3</ContainerImageTag>
	  <!--<ContainerRegistry>registry.mycorp.com:1234</ContainerRegistry>-->
	  <!--<ContainerWorkingDirectory>/bin</ContainerWorkingDirectory>-->
  </PropertyGroup>



dotnet publish --os linux --arch x64 -p:PublishProfile=DefaultContainer -c Release

The preceding .NET CLI command publishes the app as a container:

Targeting Linux as the OS (--os linux).
Specifying an x64 architecture (--arch x64).
Using the release configuration (-c Release).

Depending on the type of app you're containerizing, the command-line switches (options) might vary. For example, the /t:PublishContainer argument is only required for non-web .NET apps, such as console and worker templates. For web templates, replace the /t:PublishContainer argument with -p:PublishProfile=DefaultContainer.

ContainerBaseImage
The container base image property controls the image used as the basis for your image. By default, the following values are inferred based on the properties of your project:

If your project is self-contained, the mcr.microsoft.com/dotnet/runtime-deps image is used as the base image.
If your project is an ASP.NET Core project, the mcr.microsoft.com/dotnet/aspnet image is used as the base image.
Otherwise the mcr.microsoft.com/dotnet/runtime image is used as the base image.
The tag of the image is inferred to be the numeric component of your chosen TargetFramework. For example, a project targeting .net6.0 will result in the 6.0 tag of the inferred base image, and a .net7.0-linux project will use the 7.0 tag.


<PropertyGroup>
    <ContainerBaseImage>mcr.microsoft.com/dotnet/runtime:6.0</ContainerBaseImage>
</PropertyGroup>

ContainerRuntimeIdentifier
The container runtime identifier property controls the operating system and architecture used by your container if your ContainerBaseImage supports more than one platform. For example, the mcr.microsoft.com/dotnet/runtime image currently supports linux-x64, linux-arm, linux-arm64 and win10-x64 images all behind the same tag, so the tooling needs a way to be told which of these versions you intend to use. By default, this will be set to the value of the RuntimeIdentifier that you chose when you published the container. This property rarely needs to be set explicitly - instead use the -r option to the dotnet publish command. If the image you've chosen doesn't support the RuntimeIdentifier you've chosen, you'll get an error that describes the RuntimeIdentifiers the image does support.

You can always set the ContainerBaseImage property to a fully qualified image name, including the tag, to avoid needing to use this property at all.
docker run -it --rm -p 3000:80 --name mymicroservicecontainer my-app

<PropertyGroup>
    <ContainerRuntimeIdentifier>linux-arm64</ContainerRuntimeIdentifier>
</PropertyGroup>


ContainerRegistry
The container registry property controls the destination registry, the place that the newly created image will be pushed to. Be default it's pushed to the local Docker daemon, but you can also specify a remote registry. When using a remote registry that requires authentication, you authenticate using the well-known docker login mechanisms. See Authenticating to container registries for more details. For a concrete example of using this property, consider the following XML example:

<PropertyGroup>
    <ContainerRegistry>registry.mycorp.com:1234</ContainerRegistry>
</PropertyGroup>

ContainerImageName
The container image name controls the name of the image itself, e.g dotnet/runtime or my-app. By default, the AssemblyName of the project is used.

<PropertyGroup>
    <ContainerImageName>my-app</ContainerImageName>
</PropertyGroup>


Image names consist of one or more slash-delimited segments, each of which can only contain lowercase alphanumeric characters, periods, underscores, and dashes, and must start with a letter or number. Any other characters will result in an error being thrown.

ContainerImageTags
The container image tag property controls the tags that are generated for the image. Tags are often used to refer to different versions of an application, but they can also refer to different operating system distributions, or even different configurations. By default, the Version of the project is used as the tag value. To override the default, specify either of the following:

<PropertyGroup>
    <ContainerImageTag>1.2.3-alpha2</ContainerImageTag>
</PropertyGroup>

To specify multiple tags, use a semicolon-delimited set of tags in the ContainerImageTags property, similar to setting multiple TargetFrameworks

<PropertyGroup>
    <ContainerImageTags>1.2.3-alpha2;latest</ContainerImageTags>
</PropertyGroup>
Tags can only contain up to 127 alphanumeric characters, periods, underscores, and dashes. They must start with an alphanumeric character or an underscore. Any other form will result in an error being thrown.

ContainerWorkingDirectory
The container working directory node controls the working directory of the container, the directory that commands are executed within if not other command is run.

By default, the /app directory value is used as the working directory

<PropertyGroup>
    <ContainerWorkingDirectory>/bin</ContainerWorkingDirectory>
</PropertyGroup>

ContainerPort
The container port adds TCP or UDP ports to the list of known ports for the container. This enables container runtimes like Docker to map these ports to the host machine automatically. This is often used as documentation for the container, but can also be used to enable automatic port mapping.

The ContainerPort node has two attributes:

Include: The port number to expose.
Type: Defaults to tcp, valid values are either tcp or udp.

<ItemGroup>
    <ContainerPort Include="80" Type="tcp" />
</ItemGroup>

ContainerLabel
The container label adds a metadata label to the container. Labels have no impact on the container at runtime, but are often used to store version and authoring metadata for use by security scanners and other infrastructure tools. You can specify any number of container labels.

The ContainerLabel node has two attributes:

Include: The key of the label.
Value: The value of the label (this may be empty).

<ItemGroup>
    <ContainerLabel Include="org.contoso.businessunit" Value="contoso-university" />
</ItemGroup>
ContainerEnvironmentVariable
The container environment variable node allows you to add environment variables to the container. Environment variables are accessible to the application running in the container immediately, and are often used to change the run-time behavior of the running application.

The ContainerEnvironmentVariable node has two attributes:

Include: The name of the environment variable.
Value: The value of the environment variable.

<ItemGroup>
  <ContainerEnvironmentVariable Include="LOGGER_VERBOSITY" Value="Trace" />
</ItemGroup>

containerEntrypoint
The container entry point can be used to customize the ENTRYPOINT of the container, which is the executable that is called when the container is started. By default, for builds that create an app host, it's set as the ContainerEntrypoint. For builds that don't create an executable, the dotnet path/to/application.dll is used as the ContainerEntrypoint.

The ContainerEntrypoint node has a single attribute:

Include: The command, option, or argument to use in the ContainerEntrypoint command.
For example, consider the following sample .NET project item group:
<ItemGroup Label="Entrypoint Assignment">
  <!-- This is how you would start the dotnet ef tool in your container -->
  <ContainerEntrypoint Include="dotnet" />
  <ContainerEntrypoint Include="ef" />

  <!-- This shorthand syntax means the same thing.
       Note the semicolon separating the tokens. -->
  <ContainerEntrypoint Include="dotnet;ef" />
</ItemGroup>

