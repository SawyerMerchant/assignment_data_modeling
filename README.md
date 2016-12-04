# assignment_data_modeling
Mmmmm.... dataaaaa....

*Include your ERM modeling "pseudocode" in the space below*


John Sawyer
Catherine Khopsickle

https://docs.google.com/spreadsheets/d/1BsHGtrS-rlP_AkgB9oGwZifzUIj3FkjEFS8IE2upO6E/edit?usp=sharing


Goals	Entities	Attributes		Types		Constraints	Relationships																	
Basic 1																								
List out courses with title and description	Course	Course	title, description	Titles	string	Must be present, < 120 chars	Courses to lessons is x:x																	
Clicking a course will show a list of lessons for that course	Lesson			Descriptions	text	Must be present																		
Each lesson will have title and body		Lesson	title, body	Titles	string	Must be present, < 120 chars																		
				Body	text	Must be present																		
	Course Table:																							
	Course ID(primary key)	Title	Description	date added	date modified																			

	Lesson Table																							
	Lesson ID(primary key)	Title	Body	date added	date modified																			

	Course/Lesson Join Table																							
	CourseID(foreign key)	LessonID(foreign key)	date added	date modified																				

Basic 2																								
User credentials stored and used to log in as existing	User	Username, password digest		Username	string	Must be present, < 25 chars	User to profile is 1:1																	
Display user's matching demographics in profile	Profile	City, State, Country, Age, Gender FOREIGN KEYS		password digest	password digest	Must be present, < 25 chars, >8 Chars	Country to State is 1:x																	
Effient user input: country filters state, filters city	City						State to City is 1:x																	
Query users based on demographics	State																							
	Country																							
	Gender																							

	User Table				*User must live in a city within a state within a country																			
	User ID	User Name	Password Digest	Birthdate	*Implementation: User selects information increasingly granularly																			
	primary key	String: must be present, < 25 chars		DateTime																				

	Profile Table																							
	Profile ID	City ID (foreign key)	Gender ID (foreign key)																					
	primary key	foreign key	foreign key																					

	City Table																							
	City ID	City Name	State ID																					
	primary key	String	foreign key																					

	State/Province Table																							
	State/Province ID	State/Province Name	Abbr	Country ID																				
	primary key	String: must be present	String: optional	foreign key																				

	Country Table																							
	Country ID	Country Name																						
	primary key	String: must be present																						

	Gender Table																							
	Gender ID	Gender Name																						
	primary key	String: must be present																						


Intermediate 1																								

Add Users	Users		User:Comments 1:x																					
Users can submit Links	Links		User:Links 1:x																					
Users can submit Comments on Links	Comments		Links:L_Comments 1:x																					
Users can Comment on Comments	Favorites		Coments:C_Comments																					
Display list of Links																								
Click on Link, display hierarchy of Comments and Comments' Comments	User Table																							
View User: Links, Comments	User ID	Username	Email	Password	Added	Modified																		
	primary key	String: > 5, < 25	Email	Password Digest	Timestamp	Timestamp																		

	Links																							
	Link ID	Link URL	Link Title	Link Description	Added	Modified	User ID																	
	Primary key	String	String: >200 chars	Text: optional	Timestamp	Timestamp	foreign key																	

	Comments		polymorphic relationship/composite key																					
	Comment ID	Comment Body	Commentable (Parent) ID	Commentable (Parent) Type	User ID																			
	Primary key	Text	foreign key	String: (reference to table) Link/Comment	foreign key																			

Advanced 1																								
List of products	Products																							
List of Users and their Orders	Users																							
An Order's Shipping status	Orders																							
A Product's Order history (quantity, sale price)	Shipments																							
User's profile/Ship info/Payments	Payments																							

	Product Table																							
	Product ID	Title	Description	Stock	Price																			
	primary key	String: < 250	Text	Integer	Float																			

	Users Table																							
	User ID	Email Address	Password	Shipping Address	Billing Address																			
	primary Key	Email	Password Digest	foreign key (Address Table)	foreign key (Address Table)																			

	Address Table																							
	Profile ID	Street Address	City ID (foreign key)																					
	primary key	String	foreign key																					

		City Table																						
		City ID	City Name	State ID																				
		primary key	String	foreign key																				

		State/Province Table																						
		State/Province ID	State/Province Name	Abbr	Country ID																			
		primary key	String: must be present	String: optional	foreign key																			

		Country Table																						
		Country ID	Country Name																					
		primary key	String: must be present																					

	User Order Table																							
	Order ID	User ID	Date/Time																					
	primary key	foreign key	DateTime																					

		Order Products Table																						
		Order Product ID	Quantity	Price when ordered	Order ID	Product ID																		
		primary key	Integer	Float	foreign key	foreign key (Product Table)																		

Order Products to Shipment x:x																								
		Shipment Table																						
		Shipment ID	Shipping Method	Tracking Number	Order Product ID	Shipment Status																		
		primary key	String < 30	String: < ~30, optional	foreign key (Order Product Table)	foreign key (Shipping Status Table)																		

			Shipping Status Table																					
			Status ID	Status Code																				
			primary key	String/Int/Whatever																				

We don't save CC #'s		Payments Table																						
		Payment ID		Approval Code	Order ID	Payment Type																		
		primary key		Int <30 	foreign key (Order Table)	foreign key (Payment Type Table)																		

			Payment Type Table																					
			Type ID	Type																				
			primary key	String <30																				
