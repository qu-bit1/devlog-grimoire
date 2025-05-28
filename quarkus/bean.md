a **bean** is a _container-managed_ object that supports a set of basic services, such as injection of dependencies, lifecycle callbacks and interceptors.

you don’t control the lifecycle of the object instance directly. Instead, you can affect the lifecycle through declarative means, such as annotations, configuration, etc.

!!**exactly one bean must be assignable to an injection point, otherwise the build fails**!!