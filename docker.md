## Docker (Google)

#### Docker is good
1. Immutable achitecture: always the same all the time
2. Self contained
3. App oriented abstraction
4. Lighter weight than VMs

#### Linux containers
Usually in Linux, all the code, framework, OS, kernel, processes are available to the user when you're working in the cloud: someone just gives you a computer and it works. In Heroku etc, it's even more abstracted because you as the user own your code and your framework, and you don't really care about the OS/kernel, etc.

If you run everything in a certain container, you know EXACTLY what's going on.

Kubernetes is basically a container management system that allows you to work with Linux containers.
