# Cab_Service_Project
Cab Service University design project

__The Report CabsOnDemand.__

The task was to design a database for a cab company, I researched the project and manged to normalise it to the third form, I designed the E-R diagram and I had to create and display the queries.
This course work will help me with my next coursework in my other module of data structures and software programming where I have to develop a web app and will need to connect and design a database.
In this course I use the SQL Developer GUI, it was a new software because in the past I have tried MySQL, however I manged to get used to it and used it in my project in the end it was a lot easier to export my SQL tables using SQL developer. The research I did for this course work helped me learn and discover new technologies and websites that will help me prosper in my studies.

**Assumptions**

* They may have more than one office in the same borough
* Drivers and taxi owners are not considered to be employees
* Taxi owners provide their cars to drivers not the business
* Drivers are self employed 
* Managers are part of staff
* No two offices in the same building


**Conceptual relations.**
CabsOnDemand.
**Address**(Borough, houseNumber, StreetName, Postcode,)\
**Office**(OfficeID, MobileNos, Email, AddressID*, Telephone, Manager)\
 **Staff**(StaffNumber, FirstName, SecName, NI, D.O.B, Salary, Gender)\
**Taxi Owner**(OwnerID, FirstName, SecName, tReg)\
**Driver**(DriverID, FirstName, SecName, Gender, licenceNo)\
**Contract**(ContractID, DateSigned, DateDue, fixedCharge, NoofJobs)\
**Job**(JobID, PickupDate, PickupTime, PickupAddress, DropoffAddress, TotalChargeble, Mileage, ReasonIfFailed)\
**Client**(ClientID, ClientType(Private,(charge)Business(Businestype,email)), FirstName SecName, phoneNo))\
**Taxi**(tReg, Model, Make, Colour, Capacity, CurrentMileage, DueDate)\

**UnNormalized**\

**CabsOnDemand**(Location(Borough, houseNumber, StreetName, Postcode,), **Office**( OfficeID, MobileNos, Email, Location, Telephone, Manager), Staff(StaffNumber, FirstName, SecName, NI, Address, D.O.B, Salary, Gender), Taxi Owner( OwnerID, FirstName, SecName, tReg), Driver(DriverID, FirstName, SecName, Gender), Contract(ContractID, DateSigned, DateDue, fixedCharge, NoofJobs),Job(JobID, PickupDate, PickupTime, PickupAddress, DropoffAddress, TotalChargeble, Mileage, ReasonIfFailed), Client(ClientID, ClientType(Private,(charge)Business(Businestype,email address)), FirstName SecName Address, Contactdetaisl(MobileNo))Taxi(tReg, Model, Make, Colour, Capacity, CurrentMileage, DueDate))
Location(Borough, houseNumber, StreetName, Postcode,)
Client(ClientID, ClientType(Private,(charge)Business(Businestype,email)), FirstName SecName, phoneNo))
Contract(ContractID, officeId* DateSigned, DateDue, fixedCharge, NoofJobs)
Driver(DriverID, FirstName, SecName, Gender, licenceNO)
Job(JobID, PickupDate, PickupTime, PickupAddress, DropoffAddress, TotalChargeble, Mileage, ReasonIfFailed)
Office(OfficeID, MobileNos, Email, AddressID*, Telephone, Managerid)
 Staff(StaffNumber, FirstName, SecName, NI, D.O.B, Salary, Gender)
Taxi(tReg, Model, Make, Colour, Capacity, CurrentMileage, DueDate)
TaxiOwner(OwnerID, FirstName, SecName, tReg*)
2NF
Location(Borough, houseNumber, StreetName, Postcode,)
Client(ClientID, FirstName SecName, phoneNo))
ClientType(Private,(clientid,charge)Business(clinteid,Businestype,email))
Contract(ContractID, Jobid, officeId* DateSigned, DateDue, fixedCharge, NoofJobs)
Driver(DriverID, FirstName, SecName, Gender, licenceN0, treg)
Job(JobID PickupDate, PickupTime, PickupLocation ,DropoffLocation, Mileage, ReasonIfFailed)
JobAlloc(JobId,StaffID,DriverID,ClientiD)
Office(OfficeID, MobileNos, Email, bourogh*,Telephone, Managerid)
Staff(StaffNumber, FirstName, SecName, NI, D.O.B, Salary, Gender)
Taxi(tReg, Capacity, CurrentMileage, DueDate, driverID*)
Car (tReg, Model, Make, Colour, ownerID*) 
TaxiOwner(OwnerID, FirstName, SecName, tReg*)
3NF
Location(Borough, houseNumber, StreetName, Postcode,)
Client(ClientID, FirstName SecName, phoneNo))
ClientType(clientID,Private,(clientid,charge)Business(clinteid,Businestype,email))
Contract(ContractID, Jobid, staffId*, DateSigned, DateDue, fixedCharge, NoofJobs)
Driver(DriverID, FirstName, SecName, Gender, licenceN0, treg)
Job(JobID ReasonIfFailed)
Pickup(JobID, Date,Time,Location, priomilage)
Dropoff(JobID, time,Location, Mileage)
JobAlloc(JobId, StaffID,DriverID,ClientiD)
Office(OfficeID, MobileNos, Email, bourogh*,Telephone, Managerid)
Staff(StaffNumber, FirstName, SecName, NI, D.O.B, Salary, Gender)
Taxi(tReg,Capacity, CurrentMileage, DueDate, driverID*)
Car (tReg, Model, Make, Colour, ownerID*) 
TaxiOwner(OwnerID, FirstName, SecName, tReg*)

## Image 

![Graph](C:/Users/Shaki/Documents/GitHub/CabOnDemand/Cab_Service_Project/img/Display_1.png)

**Examples of Queries** 

SELECT OFFICE.OFFICEID, OFFICE.BOUROUGH, OFFICE.MANAGERID,PERSONA_DETAILS.FNAME, PERSONA_DETAILS.LNAME, OFFICE.TELEPHONE
FROM PERSONA_DETAILS, OFFICE
WHERE STAFFID =MANAGERID; 

SELECT DRIVERS.OFFICEID, OFFICE.BOUROUGH, DRIVERS.DRIVERID, DRIVERS.GENDER, DRIVERS.FIRSTNAME,DRIVERS.LASTNAME FROM OFFICE, DRIVERS
WHERE DRIVERS.GENDER = 'F' AND (OFFICE.BOUROUGH ='Ealing' OR OFFICE.BOUROUGH ='Islington');

SELECT TAXI.TREG, TAXI.OWNERID, TAXI.INSURANCEDATE, TAXI.CMILEAGE_1000S,TAXI.CAPACITY, HR.DRIVERS.OFFICEID, LOCATION.BOUROUGH FROM DRIVERS, TAXI, LOCATION
WHERE HR.DRIVERS.OFFICEID = 'EA09' AND
LOCATION.BOUROUGH = 'EALING'

