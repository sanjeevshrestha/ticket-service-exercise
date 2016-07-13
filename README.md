# ticket-service-exercise
## Name: Sanjeev Shrestha
##Email: sanjeevshrestha2004@gmail.com

Implement a simple ticket service that facilitates the discovery, temporary hold, and final reservation of seats within a high-demand performance venue.

Assume that the venue has a stage and one level of seating, as such:

````
        ----------[[  STAGE  ]]----------
        ---------------------------------
        sssssssssssssssssssssssssssssssss
        sssssssssssssssssssssssssssssssss
        sssssssssssssssssssssssssssssssss
        sssssssssssssssssssssssssssssssss
        sssssssssssssssssssssssssssssssss
        sssssssssssssssssssssssssssssssss
        sssssssssssssssssssssssssssssssss
        sssssssssssssssssssssssssssssssss
        sssssssssssssssssssssssssssssssss
````


The following API can be used to find and reserve seats:

````
public interface TicketService {

/**
 * The number of seats in the requested level that are neither held nor reserved
 */
  int numSeatsAvailable();

/**
 * Find and hold the best available seats for a customer
 * 
 * @param numSeats the number of seats to find and hold
 * @return a SeatHold object identifying the found seats and related information 
 */
  SeatHold findAndHoldSeats(int numSeats);

/**
 * Complete reservation of held seats
 * 
 * @param seatHoldId the seat hold identifier
 * @return a reservation confirmation code 
 */  
  String reserveSeats(int seatHoldId);
}

````

##Instructions
We've created a simple and highly-naive implemenation of the ticket service.
Your assignment is to improve the implementation by adding the following features:

1. **Seat holds expire.**  After some period of time, held seats that are not reserved are returned to the pool of available seats.
2. **Seats are assigned together.** Seats and rows are numbered. Seats are held and reserved in blocks. 

## Notes
* We would like to see a design that can scale to support multiple concurrent users. 
* *Simple is better*. For example, a lazy seat expiration model may be a good alternative to a background thread or timer.
* We understand that tradeoffs must be made to complete the exercise within the alloted time window. Do your best to document any simplifying assumptions and design considerations as you work through the problem.

##Assumptions and Solutions
Created a **Seat** domain class to hold its availability, togetherness and reservedState. This was required to find the grouped seating of the users. The **isAvailable()** method in Seat Class does the lazy check on if the seat is available or not. 
The check is done on the expiry time of the seat hold. The seat hold time is currently set to 5 second.
The grouped Seating is done in **getConsecutiveSeatsIds(int numSeats)** of  **Venue** class. This will return the ids of seats that is available for holding in blocks. 
