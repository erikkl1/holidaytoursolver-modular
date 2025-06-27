# The problem solved by the system

## Input

Someone, could be:

* a family
* a couple
* a solo traveler
* a group

wants to do a holiday tour, in e.g.:

* a country/state
* a holiday region
* a specific area
* a whole continent

He must give the number of days for planning, and decide between the two AI models and backend.

He can also give his preferences and wishes, e.g.:

* whether nature/beaches/cities
* crowded/calm
* how many stops

This should be all described through a text.

## Procedure

1. input text is sent from frontend to backend for processing
2. backend will call the Python microservice to send the text wrapped by two prompts:
    * to extract the number of days
    * to get a set of matching cities/towns
3. chosen LLM calculates the answers
4. backend will allocate the days randomly to the nonzero cities, and retrieve the cross distance matrix using db calls
5. backend gives the data to C++ microservice for TSP solving
6. backend answers to frontend: with the nonzero cities with their order and number of days of stay

During this, the frontend is also notified with events, when:

* LLM started calculating
* DB is searched
* Algo starts solving TSP

## Output

A tour going through a sequence of cities and towns:

* which is optimal in the travel time/distance if you want to visit all of them
* with days of stay
* destinations are suitable for the target demographic, fitting the preferences and in the desired region