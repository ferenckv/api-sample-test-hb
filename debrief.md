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