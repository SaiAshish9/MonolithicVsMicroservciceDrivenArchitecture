```
Evolution of Monolithic Frontends

We initially have a frontend, backend and database all embedded within
the same codebase and it's deployed the same as a whole,
this is called a monolith.

Things evolved from monolith into frontend and backend where
we split monolith into various teams.

Microservices are more specific to the backend . 
Backend evolved and people were ablt to create 
scalable architectures for backend.

For frontends , how will we scale our product with
increasing dependency, that's where microfrontends
come into picture.

We might be merging all the segments at runtime or there
can be a container application for this purpose

Micro-frontends are the microservices for the frontends (or)
scalable frontend architectures.
```

<img width="1135" alt="Screenshot 2023-03-22 at 3 26 36 PM" src="https://user-images.githubusercontent.com/43849911/226867278-ac612a08-deb1-471a-919a-8132f832191d.png">

<img width="1134" alt="Screenshot 2023-03-22 at 1 13 19 AM" src="https://user-images.githubusercontent.com/43849911/226723208-4a8f03ef-06cc-4471-b317-546e5ead0156.png">


```
Browse restaurant, surprise me and my profile
are basically three micro frontends here.

The container application is actually the root
or the feed-me page where the links to the 
microfrontends are present.
```

<img width="725" alt="Screenshot 2023-03-22 at 3 27 28 PM" src="https://user-images.githubusercontent.com/43849911/226867510-058f0f0d-21f1-45b1-931b-38db6d693eaa.png">

<img width="910" alt="Screenshot 2023-03-22 at 3 30 40 PM" src="https://user-images.githubusercontent.com/43849911/226868369-dc2f4014-4d26-479a-af98-cad6f7395a6a.png">

https://martinfowler.com/articles/micro-frontends.html

```
We'll have end to end teams which are implementing micro frontends.

Teams are segregated in terms of product which consists of FE, BE & DevOps.

This results in another pattern called BFF which is Backend for Frontend.

An upstream system is any system that sends data to the Product Master Server system. A downstream system is a system that receives data from the Product Master Server system. You can load data into the Product Master Server system at regular intervals (weekly, daily, or hourly) from an upstream system.
```

https://reflectoring.io/upstream-downstream/

<img width="742" alt="Screenshot 2023-03-22 at 3 33 15 PM" src="https://user-images.githubusercontent.com/43849911/226868939-730ddec3-0c29-4075-858b-cfbf6bb765b4.png">

<img width="815" alt="Screenshot 2023-03-22 at 3 36 24 PM" src="https://user-images.githubusercontent.com/43849911/226869743-799a8a06-bf29-49a3-834d-26b231b15d23.png">

```
Mono repo

In revision control systems, a monorepo is a software development startegy where code for
many projects are stored in the same repository.

Individual projects have separate life-cycles as opposed to one in monolithic-apps.

In case of monolithic app whole project is deployed in one go but in case of monorepos
it doen't happen the same way, we can have individual projects or products within the same repo.
with separate life cycles compared to what we had in the monolithic app, these could be individual pipelines or deployables depending on the type of individual product which we've in the same repository.

In short we've a one repository but with multiple deployables with different ways in which
we can deploy the repo. because of the presence of multiple contexts in the repo. and based on 
them deployment lifecycle changes.

Google, facebook, twitter and uber uses mono repo in same form.

Mono repo become very popular when Google declared that they are using a single monorepo for
both gmail and youtube. The whole company uses a single repository for storing all their code.

Google, Meta, Microsoft, Uber, Airbnb, and Twitter all employ very large monorepos with varying strategies to scale build systems and version control software with a large volume of code and daily changes.

Most of these use organisational monorepo as they are at the organisational level where everbody uses a same repo. for adding their code.

Spring boot, airbnb and swiggy uses project level monorepo.

Project level monorepos are seggregated as a individual product or a specific area for which we've a monorepo where we've multiple subprojects
which can be hosted in a single repository.

Spring boot is a single repository which is a project. Under vmware , we've spring boot but vmware doesn't have a single monorepo or 
organisational monorepo instead spring boot as a project has a separate monorepo.

Similarly, airbnb has a monorepo for their ui code and a monorepo for their backend code.

These are two different repository they've separated.

Tools/framework which can be leveraged for monorepos:

1. Nrwl (Next.js comes with a bundle with nrwl and nrwl can be useto create monorepos with next)
2. Lerna
3. Rush(Microsoft)
 
Microsoft created rushjs which is now called rush because they moved it into typescript.

4. Yarn Workpaces
5. Npm Workpaces
6. Google's Bazel
 
```

<img width="1082" alt="Screenshot 2023-03-22 at 4 14 20 PM" src="https://user-images.githubusercontent.com/43849911/226879645-5ee0421d-1070-4108-b387-2b7feea90d12.png">

```
Case study: Mono repos at swiggy (food delivery app):

They earlier had the dweb which is the desktop application of swiggy and mweb which is the mobile application of swiggy. So they had
two different repositories , so when we open the mobile we get a different version and at mobile, we'll get another version.

They'll served from different deployment and codebase.

They were all coverging into a nodejs based api proxy which is also known as a service-proxy and it acts as a component
between different middleware components which are hosted behind the systems.

At a high level, we've three repositories one each for dweb, mweb and service api proxy.

They were using react from frontend applications, webpack for packaging and babel for compiling js code into
final executables.

As the codebase grew swiggy recognised that they were some patterns where the code is being reused between mobile web and
desktop web application.

There was reusable code which was copy pasted and if there was a bug fix , they had to do that in both dweb and the
mweb.

In addition to that adding dependencies for react, webpack and babel becomes complicated as we keep on upgrading to
different versions, we need to updated both the repositories but they had to do two diff. deployments separately, review
them and test them separately.

It was tidious for the team to add all the common code and setup in a library as it was huge and there are multiple teams which were
working on these repositories.
```

<img width="1074" alt="Screenshot 2023-03-22 at 4 38 52 PM" src="https://user-images.githubusercontent.com/43849911/226886728-1d987864-5b25-4150-a24f-f5129edb6d14.png">


```
After they moved into monorepos , they changed the whole structure of the repository.

So there was only one repository where they had the dweb, mweb and the service proxy.

config inside repo had the webpack configuration which is reused by both the mobile and the web application.

so if we update one particular webpack under config package it will be updated to both the deployments.

They'll are in a same codebase but they are deployed as a separate artifact.

Swiggy was able to create a unified web and mobile screens using the same ui package. 
Different tenants were able to retrieve payments and reviews information from  
associated packages.

helpers are the common resuable logic which they pushed into a separte module

swiggydaily.com is pushed under daily package, there are two different components used for mobile
and web that's why there's a separate package called daily. swiggydaily.com has been stopped now.

cache has the common caching components both for the mobile and web components.

Multiple tenants can use the restaurant-url generator for the link.

One need to think much before touching the common code base.

This helped them to scale much easier. In order to build all these they're using lerna tool for building modules separately
into different components

Here are some of the pros which swiggy thinks can help them to scale the ui:
1. same fix in 1 commit
2. reusability
3. dependency updates
4. heterogeneity in ui vs mweb package
5. simpler code review

cons:
1. long bootstrap times (startup time)
2. more time for ROI
3. slower code navigation
```

https://bytes.swiggy.com/monorepos-lets-talk-about-it-4b1b7d4f1038

<img width="1121" alt="Screenshot 2023-03-22 at 4 42 51 PM" src="https://user-images.githubusercontent.com/43849911/226887526-91ed11c2-2200-4f21-ac6c-b9b6ec63a06d.png">

```
Limitations of mono repo:

1. Codebase
There going to be challenges in terms of size since monorepo can have a single codebase.
If there are too many images stored in that codebase, we need to look at the version
control system which can handle this humongous codebase. 

Google uses their own version control system as with repository size of more than 10GB, 
we can face issues with git.

2. Operational Complexity
There's going to be a lot of PRs to a single repo. and merge conflicts are going to be coming
in as there are more teams contributing to the same repository.

3. Payload Size during runtime

what if one particular feature has a version for a dependency and other feature has different version 
for other dependency. This creates longer runtime because page is going to download js files we've
diff. microfrontends serving and adding different libraries during the course of time. This adds to the
payload size and websites can be heavier in individual parts.

4. Environment Differences

When we test applications locally, we might test it in a diff. fashion and with microfrontends
we cannot deploy the whole app in the way we run it locally. So it could be more tidious
to setup microfrontends with monorepo in local compare to how we deploy to production. This may
lead to production bugs which cannot be tested at local but only at production.
```

```
Conclusion

Monorepo != Monolith

Monorepos are a way to manage multiple projects in a single repository.
Microfrontends are a useful way to read benefits of monorepo as a whole

Monorepos is not a silver bullet.

It's not going to solve all the problems which we've.

Identify why the current codebase doesn't scale and decide whether we need monorepos or not.

```

<img width="697" alt="Screenshot 2023-03-15 at 2 58 18 AM" src="https://user-images.githubusercontent.com/43849911/225140670-a00a84b3-7782-4654-b1d9-666b94a3c1fd.png">
