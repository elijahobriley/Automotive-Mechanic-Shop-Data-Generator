![[image.png]]
## Automotive Mechanic Shop Data Generator

by Elijah O.B. Riley
## Overview

TLDR;
This project generates and exports test data for an auto mechanics shop. Each record is the details of an appointment at the shop.

Each record consists of the following:
- Customer name:        The first and last name of the customer
- Customer area:          The general area where  the customer lives
- Vehicle year:               The year that vehicle was manufactured
- Vehicle model:            The make and model of the vehicle
- License plate:              The license plate  of the vehicle  (Trinidad and Tobago format)
- Appointment date:      The date on which the appointment will/did take place
- Appointment time:      The time which the appointment will/did take place
- Service:                        The service that the mechanics shop performed on the vehicle
- Service Cost:               The cost of the service

## Customer Provider
The appointment provider is used to generate data regarding the customer.

**nameGenerator()**
	The nameGenerator() function, generates a  full customer name (first and last name) using the faker library.
	eg. Kimberly Lewis

**areaGenerator()**
	The **areaGenerator()** function returns a random choice from a list of areas in Trinidad and Tobago.
	eg. Port of Spain

## Vehicle Provider
The vehicle provider is used to generate data regarding the customer's vehicle.

**manufacture_year()**
	The manufacture_year() function generates a random year between 2005 and 2020
	eg. 2009

**vehicleModel()**
	The **vehicleModel()** function returns a random choice from a list of vehicle models.
	eg. Toyota Hilux

**licence_number()**
	The **licence_number()** function generates a random licence plate number in the format of a Trinidad and Tobago licence plate. This plate is 10 times more likely to start with 'P' (a privately register car), than 'H' (a hired car, like a taxi). The second letter of the license plate starts with 'C', 'D' or 'E' to reflect most recent series of plates in Trinidad. The third letter can be any alphabetical letter except I, V, O or Q. The digits are a random digit from 1 to 9999.
	eg. PDG4521

## Appointment Provider
The appointment provider is used to generate date regarding the appointment date, time, service and the cost of the service.

**appointment_date()**
	The appointment_date() function generates a random data between today's date and 4 years from today's date.
	eg. 2022-07-16

**appointment_time()**
	The appointment_time() function generates a random time between 8AM and 3PM in 15 minute intervals. 
	eg. 12:45:00

**service_provided()**
	The service_provided() function returns a random choice from a list of services that mechanics shop provide.
	eg. Tire Rotation and Replacement

## Data frame
**generate_record()**
	The generate_record() function generates a record of the appointment details as dictionary.

A list of records is then generated using a for loop, and then the list of dictionaries (records) is converted to a pandas Dataframe.

## Clean and Sort Data
The following are done on the dataframe:
- Convert: Appointment dates are converted to datetime objects (important for sorting the records)
- Convert: Appointment times are converted to time objects (important for sorting the records)
- Remove: All records that have a license plate that already appears in the dataframe are removed
- Remove: All records that have an appointment time and date that already appears in the dataframe, are removed.

## Add service costs
The standard cost of each service is added to all records. The cost is then adjusted based on the manufacturer of the vehicle. This is done by using a dictionary that maps vehicle services to the cost the service. A new column is added that uses this dictionary to map costs into a new 'Cost' column from the 'Service' column. 

#### Adjusting the cost based on vehicle manufacturer.
In the manufacturer_factors dictionary each vehicle is mapped to a factor. The cost in each record is multiplied by the factor that is associated with that vehicle manufacturer.  
eg. a Ford Mustang's oil change will cost:
		(standard cost of oil change) x (Ford factor)
		(280) x (1.3) 
		= 364

## Export CSV file
Finally,  the dataframe is exported as a csv file.

![[Image_of_csv.png]]

banner image: [source of image](https://www.freepik.com/free-photo/medium-shot-man-checking-car_38170179.htm#fromView=search&page=3&position=13&uuid=daa046cc-e540-4431-a5a2-755a43191334)