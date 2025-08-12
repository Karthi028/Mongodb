![collections](image.png)
![alt text](image.png)
![codeketa](image.png)
![company_drives](image.png)
![mentors](image.png)
![tasks](image.png)
![topics](image.png)
![users](image.png)

1: Find all the topics and tasks which are thought in the month of October

      => db.tasks.find({date:{$gte:"2025-10-01",$lte:"2025-10-31"}});
      => db.topics.find({date:{$gte:"2025-10-01",$lte:"2025-10-31"}});

2: Find all the company drives which appeared between 15 oct-2020 and 31-oct-2020

      => db.company_drives.find({date:{$gte:"2025-10-15",$lte:"2025-10-31"}},{studentsAppeared:0});

3: Find all the company drives and students who are appeared for the placement.

      => db.company_drives.find({},{company:1,_id:0});
      => db.users.find({"placementAppeared":true},{'ProblemSolved':0});

4: Find the number of problems solved by the user in codekata

      => db.codekata.find({},{"date":0});

5: Find all the mentors with who has the mentee's count more than 15

      => db.mentors.find({menteeCount:{$gte:15}});

6: Find the number of users who are absent and task is not submitted  between 15 oct-2020 and 31-oct-2020

    => db.tasks.aggregate([
    {
        $match:{
            date:{$gte:"2025-10-15",$lte:"2025-10-31"}
        }
    },
    {
        $group:{
            _id:null,
            "No of users not submitted task":{$sum:"$No of notsubmittedtask users"}
        }
    }
    ]);

    => db.attendance.aggregate([
    {
        $match:{
            date:{$gte:"2025-10-15",$lte:"2025-10-31"}
        }
    },
    {
        $group:{
            _id:null,
            totalabsent:{$sum:'$NoofAbsents'}
        }
    }
    ]);
