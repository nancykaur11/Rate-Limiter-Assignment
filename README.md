# Rate-Limiter-Assignment

The objective of this project is to implement a Sliding Window Rate Limiter.
The objective of the system is to limit the number of requests each user can make during a time period.

For example:
A user can make 5 requests within 60 seconds.
If the user exceeds this limit, further requests should be rejected until the window allows more requests.

## Approach

The Sliding Window Algorithm is being implemented as the approach for this project.
The algorithm continuously checks the number of requests made during the last N seconds prior to the current time.

For each incoming request where:
- Remove all requests that are older than the allowed time window.
- Count remaining requests.
- If count is less than limit -> allow request.
- If count reaches limit -> reject request.

This will allow for accurate and timely tracking of the rates that users make.

## Data Structure

Two main data structures are used in this implementation.

a) A Queue is used to maintain the timestamps of requests from each user.
- A Queue is used because:
- Requests must be processed in the order they were received.
- Should process the oldest request first.
- A Queue has a FIFO (First In First Out) property, which will work perfectly for this requirement.

b) A Map is used to associate Queues with identifiers for users.
- A Map is used to store queues for different users.
- Each user has their own independent request tracking.

## q 

q represents the queue for a specific user.
When a request comes:
- We fetch that user  queue from the map.
- If it does not exist, we create one.
- We then remove expired timestamps from q.
- we check if the request can be allowed.

So q is simply the user request history within the current time window.

## Flow 

For every request:
- Get the current time.
- Calculate the start of the valid window.
- Fetch the user's queue.
- Remove outdated timestamps.
- Check if request count reached limit.
- If not, add current timestamp and allow request.
