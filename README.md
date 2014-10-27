607week9MongoDb
===============

#1) creating a new MongoDB database called employment:
use employment

#2) Insert a new record for Wendy Yasquez into the database and into a collection called employees.

db.employees.insert({Name:"Wendy Yasquez", Title:"Assistant Professor", Salary:86000,Department:"Computer Science",Hire_Year:1998})


#3) Write a JavaScript function to insert new professors into the employees collection.

function InsertProf(Name,Title,Salary,Department,Hire_Year) {
db.employees.insert ({Name:Name,Title:Title,Salary:Salary,Department:Department,
Hire_Year:Hire_Year});
}


#4)
Use this function to insert the records for Raoul Dewan, Isabelle Winters, and Jack McDunn.

InsertProf("Raoul Dewan", "Assistant Professor", 78000,["Physics", "Biology"],2009);

InsertProf("Isabelle Winters", "Associate Professor", 92000,"Physics",1995);

InsertProf("Jack McDunn", "Associate Professor", 101000,"Physics",1993);

#5)
function InsertAdEmployee (Name,Title,Salary,Division,Location,Hire_Year) {
db.employees.insert ({Name:Name,Title:Title,Salary:Salary,Division:Division,
Location:Location,Hire_Year:Hire_Year});
};
# 6.a) Use this function to insert the records for Tonja Baldner and Dennis Bohnet.
InsertAdEmployee("Tonja Baldner", "Assistant to the Dean", 42000,"Arts and Sciences",null,2001);
#6.b)
InsertAdEmployee("Dennis Bohnet", "Vice President", 106500,"Academic Affairs","Main Campus", 1997);

#7) Show the code that will return all employees with salaries less than $90,000.

db.employees.find({Salary:{$lt:90000}});

#8)Show the code that will return all professors with salaries less than $90,000.

db.employees.find({Title:/Professor/ , Salary:{$lt:90000}});

#9) Show the code that will return all Physics professors hired before 2001.

db.employees.find({Title:/Professor/ , Department:/Physics/  , Hire_Year: {$lt:2001} });

#10) Show the code that will return all professors who teach for departments other than Physics.


db.employees.find({Title:/Professor/ , Department: {$nin: ['Physics'] } });


#11) Show the code that will return all employees who were either hired before 1997 or who
have salaries greater than $100,000.


db.employees.find({ $or: [ {Hire_Year: {$lt:1997} }  , {Salary:{$gt:100000} }   ] } );


#12) Suppose Tonja Baldner has been given a 10% raise. Show the code that will update her
salary correctly.


db.employees.update({Name:"Tonja Baldner" },{$mul: {Salary:1.1}});


##13) Professor Dewan has been offered a job at another university. Show the code that would
//remove his record from the database.


db.employees.remove({ Name: "Raoul Dewan" } );


#14) Instead of removing Professor Dewan’s record, we might prefer to create a new collection
//called pastemployees and move his record there. Show the code that will move his record to the new collection and add a departyear value of 2014 to his record. (You can do it in two steps.)
# create collection
db.createCollection(“PastEmployees”);
# first I will clone the collection from employees to PastEmployees and restricted to Raoul Dewan
db.employees.find({Name:"Raoul Dewan"}).forEach(function(x){db.PastEmployees.insert(x)});

# I delete Raoul from employees
db.employees.remove({Name:"Raoul Dewan"});
# I update PastEmployees collection to add a field for Depart_Year
