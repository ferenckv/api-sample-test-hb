# How to Improve this project

## Performance

### Problem
1. Multiple calls to Hubspot to get the same info. For example, contacts.

### Solution
1. Cache the results. To achieve this, the order of the operations shoud be altered. First you would have to get all the modified objects (Companies, Contacts, Meetings, etc) process them and get the list of objects and associations to be retrieved from Hubspot. Finally, associate the modified objects with the extra details obtained from the API and store the actions in the DB.

## Code readability

### Problem
1. The worker file is doing too much. Also, the external dependencies (from /utils, from example) are not really well separated in terms of logical agrupation.

## Solution
1. Refactor the code. Separate into different files and/modules:

   1.1 Logic to control the queue.

   1.2 Logic to query Hubspot API.

   1.3 Logic to process the data extracted from Hubspot API.

   1.4 Logic to create and insert actions into the DB.

## Code quality

### Problem
1. Multiple entangled dependencies. Repetitive code. Magic strings.

### Solution
1. Some sort of basic SOLID? principles compilance.

   1.1 Single responsibility: See solution from previous section.

   1.2 Dependency inversion: Passing the domain object around is a good start, but after refactoring, more of this will be needed.

# About the implementation tradeoffs

When dealing with an existing codebase, I always try to follow a few good practices:
1. Identify and follow existing patterns.

   1.1 The way the `lastPulledDates` are stored

   1.2 The way data is extracted from Hubspot

   1.3 The way the extracted data is processed

   1.4 The way the actions are queued to be sent to the db in batches

2. Improve existing antipatterns and code smells. 

    2.1 Everything I'm listing in the previous section can be improved. However, I choose not to make any changes to comply with the 2 - 3 hours expectation.

    2.2 With some extra time, I would have encapsulated some of the repetitive code in helper functions and I would have extracted some logic away from the main `worker.js` file.
   