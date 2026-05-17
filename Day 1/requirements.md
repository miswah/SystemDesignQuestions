# URL Shortener

## 1. Functional Requirements

    * shorten URL
      * Accept a long url as input
      * Generate a unique short url
    * Redirect
      * When user access a short URL redirect to the original long URL
    * Analytics
      * Track click count, location, device type, etc put as a book.
    * API Access
      * Provide API for programmatic creation and management of URLs

----

## 2. Non-Functional Requirements
    * Low Latency
      * Redirection should happen quickly (50-100 ms)
    * High Availability 
      * Should be available at least 99.99%
    * Scalability
      * Must support millions to billions of requests
      * System is read heacy (100:1 read/write ratio)


## Once a short URL is created it should remain valid for its lifetime

## Estimations
* 100 m new URLs per month
* Read heavy workload (100:1 read/write ratio)
* write per second -> 40 requests
* read per seconds -> 4000 requests

# Large Scale
* writes 230 requests per second
* read 230000 requests per second
