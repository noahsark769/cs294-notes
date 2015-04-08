## Docker (Google)

#### Docker is good
1. Immutable achitecture: always the same all the time
2. Self contained
3. App oriented abstraction
4. Lighter weight than VMs

#### Linux containers
Usually in Linux, all the code, framework, OS, kernel, processes are available to the user when you're working in the cloud: someone just gives you a computer and it works. In Heroku etc, it's even more abstracted because you as the user own your code and your framework, and you don't really care about the OS/kernel, etc.

If you run everything in a certain container, you know EXACTLY what's going on.

Kubernetes is basically a container management system that allows you to work with Linux containers. "Declarative framework for container orchestration." You give kubernetes a desired state of the system, and it figures out how to get to the desired state from the current state of the system. Something you can assert and walk away from. This is especially cool because if something crashes on the system that makes it different from the desired state, it will be able to get back to the desired state (or at least try to).

#### Kubernetes Architecture
etcd: a tiny OS for a containerized world. Built by startup called Core OS. In etcd you can have paths like /foo/bar/baz mapping to pieces of data (which cannot be large (?)). Basically a KV store.

Used for optimistic concurrency and watch. Optimistic distributed concurrency (ODC): system in which you can have concurrency without locks, like a transaction based system. Not really sure how this works...? But apparently you can do distributed concurrency without having distributed lock systems. Can do compare&swap, read-update-write without races. Also: write with precondition - you can say to reject the write if the read is not what you think it will be.

Watch: a hanging GET. Hanging GET is a "beautiful hack" - you can do an HTTP GET where you don't terminate the connection, so when new data packets come in you can display them as push notifications, basically. Cute, I didn't know about this. Used to implement watch.

Off of etcd, you have an API server which is daemon and user facing. Daemons for scheduler and controller manager also use this API - this is nice because the API Server will be able to reconcile version differences.

Kubernetes scheduler: takes VMs (or phys machines too) and turn them into a "unified compute substrate", which is a fancy word for a large pool of resources. Similar to multiple cores. Like an OS scheduling processes on cores, but scheduling process on VMs instead. "I want to run this on 3.0 cores with 5GB of RAM, find me a place to run it." *Spreading* to minimize the destruction if one machine scales. If you have lots of jobs of the same group, spread it over multiple machines (or failue domains). Even utilization to try to keep load equal on all machines.

What's the thing that we "schedule"? It's called a pod, and it's a collection of one or more containers which share IP address, other namespaces, volumes (?) etc. Pod is the atomic unit of scheduling, not container, because it's oftentimes the best to pair up containers to work together and depend on each other.

Replication manager: cookie cutter, number, and label query. "I want to replicate this image (cookie) this many times (number)." The label query is something which is able to find certain instances based on a unique label. Will kill pods if there are too many running right now, add new ones if there are too few running right now. Adding new ones will associate the label query with the new machines, I think.

Service: abstraction layer between frontends, middleware, backends etc. Can handle internal virtual IP addresses etc in order to provide MORE abstraction. We really love abstraction here. Frontend exposes the same IP address, but the service is balancing backend machines which are going up and down.

##### Dynamic vs. Static queries
You have a job that you want to run, with tasks. Cannot remove tasks from a job because it only works within the job. The problem is if a job is automatically killed and replaced by the system then it's hard to debug why it crashed. Instead, what we can do is strip the prod label from a job (machine) that crashes, and creates a new one. Can even send out a ticket with a link to log into the live server that is sick and not responding to prod requests anymore.
