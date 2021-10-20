# System Design Interview Practice
This repository contains notes for preparing for System Design Interviews. I will also host my Draw.io diagram for practice using this repository.

### Intro
In a SWE interview process, the system design round has become a standard part of the interview. If you want to get your dream job in some big tech giant companies (especially as a Senior Engineer), then you need to tell your approach about building a complex, large scalable system.
Note that there is no standard or accurate answer to the design interview questions.

### Top 10 System Design Interview Questions and Answers
Link:
https://www.geeksforgeeks.org/top-10-system-design-interview-questions-and-answers/

  1. Design a URL Shortening Service (TinyURL)
    - URL shortening service allows users to enter a long URL, and then it returns a shorter, unique URL. Examples include bit.ly and TinyURL. These services generate a short URL if the user gives a long URL and if the user gives a short URL then it returns the original long URL.
    - Things to discuss and analyze:
      - Given a long URL, the service should generate a shorter and unique alias of it.
      - When the user hits a short link, the service should redirect to the original link.
      - Consider scalability if 1000's of URL shortening requests are coming each second.
      - Service handle redirects.
      - Support for custom short URLs.
      - Track click statistics.
      - Delete expired URLs.
      - System should be highly available.
    - Need to consider three things when designing this service:
      a. API (REST API) - Discuss how client will follow an approach to communicate w/ the service along w/ load balancer which is the front end of the service.
      b. Application Layer - Discuss how the worker thread or hosts that will take the long URL, generate the tiny URL and how it will store both of the URLs in the database.
      c. Persistence Layer - Database.

      
  2. Design Youtube/Netflix (Global Video Streaming Service)
    - Design a video streaming service like Youtube/Netflix where users can upload/view/search videos. The service should be scalable where a large number of users can watch and share the videos simultaneously. It will be storing and transmitting petabytes and petabytes of data.
    - Things to discuss and analyze:
      - Approach to record stats about videos, e.g., the total number of views, up-votes/down-votes, etc.
      - Adding comments on videos in real-time.
    - Components:
      - OC - Clouds like AWS (CloudFront), OpenConnect which acts as a content delivery network. Recall that a content delivery network is a geographically distributed group of servers that work together to provide fast delivery of Internet content.
      - Backend - Database
      - Client - Any device to use Youtube/Netflix.

  3. Design Facebook Messenger or WhatsApp (A global chat service)
    - Approach for one-on-one text messaging between users.
    - Approach for extending the design to support group chats.
    - Delivered and read status.
    - What action needs to be taken if the user is not connected to the internet, i.e. save the message as a draft, delete message, or specify/schedule another time to send the desired message.
    - Push notifications. Also, there should be some option s.t. one can remove push notifications to improve focus.
    - Sending media like images or other documents.
    - Approach for providing end-to-end message encryption.


  4. Design Quora/Reddit/HackerNews (A social network + message board service).
    - Theses services allow users to post questions, share links and answerr the questions of other users.
    - Users can also comment on questions or shared links.
    - Things to discuss and analyze:
      - Approach to record statistics of each answer such as number of views, up-votes/down-votes, etc. I.e., create a posts table, comments and shared links table. There can be comment_id in posts table connected to comments table as an example of a relationship.
      - Follow options should be there for users to follow other users or topics.
      - News feed generation which means users can see the list of top questions from all the users and topics they follow on their timeline.


  5. Design Search Typeahead
    - Typeahead service allows users to type some query based on that it suggests top searched items starting w/ whatever the user has typed.
    - Things to discuss and analyze:
      - Approach to store previous search queries
      - Real time requirement of the system
      - Approach to keep the data fresh
      - Approach to find the best matches to the already typed string
      - Queries per second to be handled by the system
      - Criteria for choosing the suggestions
      - Total number of data to be stored
      - Approach to find the best matches to the already typed string


  6. Design Dropbox/Google Drive/Google Photos (Global File Storage and Sharing Service)
    - Design a file or image hosting service which allows users to upload, store, share, delete and download files or images on their servers and provides synchronization across various devices.
    - Service should support automatic synchronization between devices, i.e., after updating a file on one device, it should get syncrhonized on all devices.
    - ACID (Atomicity, Consistency, Isolation and Durability) property should be present in the system.
    - Approach to track permission for file sharing.
    - Allowing multiple users to edit the same document.
    - System should support storing large files up to a specified amount of GB.

  7. Design a Web Crawler
    - Design a Web Crawler scalable service which collects information (crawl) from the entire web and fetches hundreds of millions of web documents.
    - Things to discuss and analyze:
      - Approach to find new web pages.
      - Approach to prioritize web pages which change dynamically (new content is provided every time a user views it).
      - Ensure that the crawler is not unbounded on the same domain.

  8. Design Facebook, Twitter or Instagram
    - Need to design a social media service for billions of users.
    - Most of the interviewers will spend time in the discussion of news feed generation service in these apps.
    - Features to be considered:
      - Some of the specific Twitter/Facebook/Instagram features to be supported.
      - Privacy controls around each tweet or post.
      - User should be able to post tweets also the system should support replies to tweets/grouping tweets by conversations.
      - User should be able to see trending tweets/post.
      - Direct messaging.
      - Mentions/Tagging.
      - User should be able to follow another user.
    - Things to analyze:
      - System should be able to handle the huge amount of traffic for billions of users (i.e. apply CDN (Content Delivery Network) to access websites that are down due to heavy traffic).
      - Number of followers.
      - Number of times the tweet has been favorited.
    - Components:
      - News feed generation
      - Social graph (Friend connection networking between users or who follows whom? - ? especially when millions of users are following a celebrity or 1st, 2nd and 3rd degree connections for a given LinkedIn user).
      - Efficient storage and search for posts or tweets.

  9. Design Uber or Lyft
    - Design a service where a user requests a ride from the app, and a driver arrives to take them to their destination.
    - A frequently asked interview question in system design round of interviews.
    - Architecture: Monolithic (Traditional unified model for the design of a software program)/Microservices (Real-time service, front-end (application) and database)
      - Example of Monolithic eCommerce SaaS application may contain a web server, a load balancer, a catalog servich which services up product images, an ordering system, a payment function and a shipping component.
      - Monolithic vs. Microservices: While a monolithic application is a single unified unit, a microservices architecture breaks it down into a collection of smaller independent units. Units carry out application process as a separate service. In other words, using a single vs. multiple service to carry out important tasks.
    - Things to analyze and discuss:
      - Backend is primarily serving mobile phone traffic. Uber application talks to the backend over mobile data.
      - How dispatch system works (GPS/locations data is what drives the dispatch system)
      - How do we efficiently match the user requests w/ the nearby drivers?
      - How do maps and routing work in Uber? How ETAs are calculated?
      - An efficient approach to store millions of geographical locations for drivers/riders who are always on the move.
      - Approach to handle millions of updates to a driver location.
      - Dispatch is mostly built using Node.js.
      - Figure out a way to automatically calculate the desired pay and tip for an Uber driver based on the requested user destination and current location (work w/ shortest path algorithm to find minimum distance and multiply by a certain value to scale out the Uber driver pay). Write this program out in Python.
      - Services: Business logic services mostly written in Python.
      - Databases: Postgres, Redis, MySQL

      - Think how this would help me think in regards to the TuSimple self-driving truck company. I need to think about front-end, back-end, and database services. On the client side, the driver of the self-driving truck can have an option that will allow the truck to go into self-driving mode s.t. the driver can rest. We need to write a Python program at scale which will keep track of nearby vehicles, road/street data, speed of nearby vehicles to know when to stop or best alternative reaction to a dangerous driver, checks for blind spots (i.e. a motorcyclist on the blind spot), and proceeds to drive in a safe manner.
      - The backend service will be used to automatically drive the vehicle once triggered by the driver to place into self-driving truck mode. Self-driving truck mode is only available w/ a truck driver in place, so you must also have your system set up to store immediate user and passwords and the beginning of your driving session.
      - The database service involved can be a NoSQL database solution such as AWS DynamoDB to store real-time data of surrounding vehicles, current vehicle and roadmap to figure out best response to deal with potential hazards and accidents.
      - To scale up the solution, we can use something like AWS CloudFront as a content delivery network to provide essential information with respect to heavy traffic (literally) and requests.


  10. Design an API Rate Limiter
    - Design a service or tool which monitors the number of requests per a window time a service agrees to allow.
    - If the number of request exceeds, the rate limiter blocks all the excess calls.
    - Things to analyze and discuss:
      - Limiting the number of requests an entity can send to an API within a time window, for example, twenty requests per second.
      - Rate limiting should work for a distributed setup, as the APIS are available through a group of servers.
      - How to handle throttling (soft and hard throttliing, etc.)
    - Note:
      - Throttling is a process used to control the usage of APIs by consumers during a given period. 
       Hard --> Number of API requests cannot exceed the throttle limit. 
       Soft --> You can set the API request limit to exceed a certain percentage.
      - Rate-limiting is a process used to define the rate/speed at which consumers can access APIs.



















