# MongoDB-Assignment-1

### Create ToDo List
db.todos.insertMany([
  { 
    task: "complete EC2", 
    due_date: new Date("2025-05-01"), 
    status: "completed" 
  },
  { 
    task: "Complete IAM", 
    due_date: new Date("2025-05-05"), 
    status: "completed" 
  }
])

![image](https://github.com/user-attachments/assets/8991d279-d518-4054-a37b-03f1a2f88603)

### View ToDo List
db.todos.find({})

![image](https://github.com/user-attachments/assets/c6b434b0-6319-4486-a3b2-38689553107d)


### Change datatype of status from strings to boolean
db.todos.updateMany(
  { status: "completed" },
  { $set: { status: true } }
)

db.todos.updateMany(
  { status: "pending" },
  { $set: { status: false } }
)

![image](https://github.com/user-attachments/assets/38a85e9b-4305-4994-bff9-8c174a901592)


### Insert more ToDos
db.todos.insertMany([
  {
    task: "Learn S3",
    due_date: new Date("2025-06-01"),
    status: false
  },
  {
    task: "Practice Lambda",
    due_date: new Date("2025-06-05"),
    status: false
  },
  {
    task: "Review CloudWatch",
    due_date: new Date("2025-06-10"),
    status: true
  }
])

![image](https://github.com/user-attachments/assets/d2363800-f57c-4336-90d0-05d2ab16b3fa)


### Set default status to false
function addTodo(task, due_date) {
  db.todos.insertOne({
    task: task,
    due_date: new Date(due_date),
    status: false
  });
}



### Change status using object id
db.todos.updateOne(
  { _id: ObjectId("your_object_id_here") },
  { $set: { status: false } }
)

![image](https://github.com/user-attachments/assets/77aeca5c-dda3-4c43-bb00-96c6e17c367e)



### Add a priority field using enum
db.runCommand({
  collMod: "todos",
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["task", "due_date", "status", "priority"],
      properties: {
        task: { bsonType: "string" },
        due_date: { bsonType: "date" },
        status: { bsonType: "bool" },
        priority: {
          enum: ["High", "Medium", "Low"]
        }
      }
    }
  },
  validationLevel: "strict"
})

![image](https://github.com/user-attachments/assets/112031a2-dc25-489a-b971-bea458b6e872)


### Insert with Priority
db.todos.insertOne({
  task: "Set up CloudFront",
  due_date: new Date("2025-06-30"),
  status: false,
  priority: "Low"
})



### Sort on due date
db.todos.find().sort({due_date:1})

![image](https://github.com/user-attachments/assets/24432efb-fe9b-43b2-b160-5d28391d5a7e)



### Find pending tasks for specified date
db.todos.find({
  status: false,                         
  due_date: { $lt: new Date("2025-06-10") }  
})

![image](https://github.com/user-attachments/assets/a297a938-539f-4380-97c8-82f80246c182)



### Count tasks
db.todos.countDocuments()

![image](https://github.com/user-attachments/assets/4677ffb7-57a8-4ae4-9291-007626f7e5d3)






