## Code Portfolio Overview
*Last updated: 2023-10-03*

Hello! Thanks for dropping by. This page gives some of the background and motivation to some my coding projects to help you understand how they relate to my interests and broader projects. 

Early development projects can be a bit of a mess and might not yet be runnable, but give a sense of the direction they're heading and the logic used. For these I've provided a link to the branch that is most current.

### [test-site](https://www.github.com/kphang/test-site) Python app (stable)
This FastAPI set of mock endpoints was developed to help test another app I was developing called BADGER (see below). The goal was to test the optimization of rate limiting strategies against a site with an unknown rate limit.

The test-site app uses a customizable file to implement rate limiting, period quotas, max concurrency, and throttling applied after rate/quota are exceeded. It also allows introducing a random delay to simulate response delay times that would exist from a remote server.


### [BADGER](https://github.com/kphang/BADGER/tree/kphang/issue2) Python web app (early development)
**B**atch **A**PI **D**ata-requests, **G**et **E**ventual **R**esults. A FastAPI web app utilizing httpx, anyio, jinja templates, and a sqlite backend, meant to to run in a docker container (and optionally kubernetes).

The idea behind this app came from a need to request a large set of data from a service with a monthly quota over an extended period for a data science project. This would require me to manually group my requests, set a reminder to resume my requests each month, and finally concatenate my results at the end. Instead I decided to make a generalized app to perform the task, in hopes that it might also be of benefit to data scientists/engineers.

This plan for this app is to allow you to upload a job containing a set of requests to endpoints and schedule them to run in batches (e.g. 1,000/month starting October 1, 2023). Requests are sent asynchronously to maximize completion speed, but also utilize exponential backoff and concurrency limits in order to not overwhelm the receiving service, and ensure rate limits are adhered to. Failed requests will be rerun a set number of times. After each batch completion the results are appended to the file associated with the job. Multiple jobs can be scheduled each with their own schedules. Notifications will be generated on problems or job completion.


### [xvarmap](https://github.com/kphang/xvarmap/tree/dev) Python package (early development)
The impetus for this package was the result of working with StatCan's census products, which have no convenient way of mapping variables over multiple years. Because variable id's change over time due to the introduction/removal of questions, joining based on the id generated errors. Similarly, question descriptions are duplicated (e.g. English) or inconsistent (e.g. Population 2016, Population 2011), preventing it from being used as a basis for joins.

The intention of this package is to create tools to detect and automatically correct potential mismatches, based on description diffs resulting from the joining of disconnected variable id's. As well, the goal is to provide tools to conveniently remap variable id's using a limited wrapper around pandas to ensure that certain formatting requirements are met to ensure the added functions generate valid transformations. The result of using this package is the generation of a mapping file that can be shared with others to transform the datasets consistently. This mapping file can also serve as API change documentation.

